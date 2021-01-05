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

var calendarEl = document.getElementById('calendar');
var calendar = new FullCalendar.Calendar(calendarEl, {
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
        el.title = event.extendedProps.meeting.meeting_type;
    },
});
calendar.render();
</script>