<h1>RCOS Calendar</h1>

<div id='calendar'></div>

<script>
const meetingColors = {
    'large_group': '#da291c',
    'small_group': 'green',
    'presentations': 'orange',
    'bonus_session': 'gold',
    'grading': 'red',
    // 'mentors': ''
    'coordinators': 'purple'
    // 'other'
};

function meetingToEvent(meeting, index) {
    return {
        title: (meeting.title || 'Meeting'),
        start: meeting.start_date_time + 'Z',
        end: meeting.end_date_time + 'Z',
        backgroundColor: meetingColors[meeting.meeting_type],
        meeting
    }
}

const apiBaseUrl = 'http://198.211.105.73:3000';
const tooltip = document.getElementById('tooltip');
const calendarEl = document.getElementById('calendar');
const calendar = new FullCalendar.Calendar(calendarEl, {
    initialView: 'dayGridMonth',
    timeZone: 'America/New_York',
    weekends: false,
    events: function(info, successCallback, failureCallback) {
        fetch(apiBaseUrl + '/meetings')
            .then(res => res.json())
            .then(meetings => successCallback(meetings.map(meetingToEvent)))
            .catch(failureCallback)
    },
    eventDidMount ({ event, el }) {
        const { meeting } = event.extendedProps;
        const meetingType = meeting.meeting_type.split('_').join(' ');
        const hostString = meeting.host_username ? ` hosted by ${meeting.host_username}` : '';
        const agendaString = meeting.agenda ? `<div class='meeting-agenda'><strong>Agenda</strong><ul>${meeting.agenda.map(item => '<li>' + item + '</li>').join('\n')}</ul></div>` : '';
        const location = meeting.location && meeting.location.includes('http') ? `<a href='${meeting.location}' target='_blank'>${meeting.location}</a>` : meeting.location;
        let locationString = '';
        if (meeting.location && meeting.location.startsWith('http')) {
            locationString = `<a target='_blank' href='${meeting.location}'>${meeting.location}</a><br>`;
        } else if (meeting.location) {
            locationString = `<span class='meeting-location'>${location}</span><br>`;
        }
        const presentationString = meeting.presentation_url ? `<a class='meeting-presentation-url' href='${meeting.presentation_url}' target='_blank'>Presentation</a>` : '';
        const recordingString = meeting.recording_url ? `<a class='meeting-recording-url' href='${meeting.recording_url}' target='_blank'>Recording</a>` : '';
        
        tippy(el, {
            allowHTML: true,
            interactive: true,
            theme: 'light',
            content: `
                <strong class='meeting-title'>${meeting.title}</strong><br>
                <p class='meeting-type' style='text-transform: capitalize'>${meetingType} Meeting${hostString}</p>
                ${agendaString}
                ${locationString}
                ${presentationString}
                ${recordingString}
            `,
        });
    },
});
calendar.render();
</script>