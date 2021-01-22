<h1>RCOS Calendar</h1>

<div id='calendar'></div>

<script>
const meetingColors = {
    'large_group': '#da291c', // RCOS red
    'small_group': 'green',
    'presentations': 'orange',
    'bonus_session': 'gold',
    'grading': 'red'
};

/** Maps a meeting object from the API into a Fullcalendar event. */
function meetingToEvent(meeting, index) {
    const event = {
        title: (meeting.title || 'Meeting'),
        start: meeting.start_date_time + 'Z',
        end: meeting.end_date_time + 'Z',
        backgroundColor: meetingColors[meeting.type],
        meeting
    };

    // TODO: if this is not set, point to RCOS meetings url for auto-generated slides
    if (meeting.external_presentation_url) {
        event.url = meeting.external_presentation_url;
    }

    return event;
}

// Points to RCOS Postgrest API
const apiBaseUrl = 'http://198.211.105.73:3000';

const calendarEl = document.getElementById('calendar');
const calendar = new FullCalendar.Calendar(calendarEl, {
    initialView: 'dayGridMonth', // Classic calendar view
    timeZone: 'America/New_York',
    weekends: false, // Change this to true if RCOS might have weekend events
    events: function(info, successCallback, failureCallback) {
        fetch(apiBaseUrl + '/public_meetings')
            .then(res => res.json())
            .then(meetings => successCallback(meetings.map(meetingToEvent)))
            .catch(failureCallback)
    },
    eventDidMount ({ event, el }) {
        // For each event, construct the HTML content of a tooltip
        try {
            // Full meeting object from API is stored in extendedProps
            const { meeting } = event.extendedProps;
            
            // Turns 'large_group' into 'large group'
            const meetingType = meeting.type.split('_').join(' ');
            
            // Meetings might have a host username
            const hostString = meeting.host_username ? ` hosted by ${meeting.host_username}` : '';
            
            const agendaString = meeting.agenda ? `<div class='meeting-agenda'><strong>Agenda</strong><ul>${meeting.agenda.map(item => '<li>' + item + '</li>').join('\n')}</ul></div>` : '';
            
            // Location might be empty, a phsyical location, or a URL
            let locationString = '';
            if (meeting.location && meeting.location.startsWith('http')) {
                locationString = `<a target='_blank' href='${meeting.location}'>${meeting.location}</a><br>`;
            } else if (meeting.location) {
                locationString = `<span class='meeting-location'>${location}</span><br>`;
            }

            // External presentation will not always be present
            const presentationString = meeting.external_presentation_url ? `<a class='meeting-presentation-url' href='${meeting.external_presentation_url}' target='_blank'>Meeting Slides</a>` : '';
            
            // Recording URL will not always be present
            const recordingString = meeting.recording_url ? `<a class='meeting-recording-url' href='${meeting.recording_url}' target='_blank'>Recording</a>` : '';
            
            tippy(el, {
                allowHTML: true, // allows content to have HTML
                interactive: true, // keeps the tooltip open when mouse hovers over the tooltip
                theme: 'light', // closest to RCOS theme
                content: `
                    <strong class='meeting-title'>${meeting.title}</strong><br>
                    <p class='meeting-type'>${meetingType} Meeting${hostString}</p>
                    ${agendaString}
                    ${locationString}
                    ${presentationString}
                    ${recordingString}
                `,
            });
        } catch (e) {
            // By default errors are ignored in this callback for some reason, so we want to make sure they are logged if they occur
            console.error(e);
        }
    },
});
calendar.render();
</script>