<h1>RCOS Calendar</h1>

<div id="calendar"></div>

<script>
const meetingColors = {
    "large_group": "#da291c",
    "small_group": "green",
    "presentations": "orange",
    "bonus_session": "gold",
    "grading": "red",
    // "mentors": ""
    "coordinators": "purple"
    // "other"
};

function meetingToEvent(meeting, index) {
    return {
        title: (meeting.title || "Meeting"),
        start: meeting.start_date_time + "Z",
        end: meeting.end_date_time + "Z",
        backgroundColor: meetingColors[meeting.meeting_type],
        meeting
    }
}

const tooltip = document.getElementById('tooltip');
const calendarEl = document.getElementById('calendar');
const calendar = new FullCalendar.Calendar(calendarEl, {
    initialView: 'dayGridMonth',
    timeZone: 'America/New_York',
    weekends: false,
    events: function(info, successCallback, failureCallback) {
        fetch("https://rcos-api.herokuapp.com/api/v1/meetings/")
            .then(res => res.json())
            .then(meetings => successCallback(meetings.map(meetingToEvent)))
            .catch(failureCallback)
    },
    eventDidMount ({ event, el }) {
        const { meeting } = event.extendedProps;
        const meetingType = meeting.meeting_type.split("_").join(" ");
        const hostString = meeting.host_username ? ` hosted by ${meeting.host_username}` : "";
        const agendaString = meeting.agenda ? `<strong>Agenda</strong><p>${meeting.agenda}</p><br>` : "";
        const location = meeting.location && meeting.location.includes("http") ? `<a href="${meeting.location}" target="_blank">${meeting.location}</a>` : meeting.location;
        const locationString = meeting.location ? `<span>${location}</span><br>` : "";
        const presentationString = meeting.presentation_url ? `<a href="${meeting.presentation_url}" target="_blank">Presentation</a>` : "";
        const recordingString = meeting.recording_url ? `<a href="${meeting.recording_url}" target="_blank">Recording</a>` : "";
        
        tippy(el, {
            allowHTML: true,
            interactive: true,
            theme: 'light',
            content: `
                <strong class="meeting-title">${meeting.title}</strong><br>
                <em style='text-transform: capitalize'>${meetingType}${hostString}</em><br>
                ${agendaString}
                <br>
                ${locationString}
                ${presentationString}
                ${recordingString}
            `,
        });
    },
});
calendar.render();
</script>