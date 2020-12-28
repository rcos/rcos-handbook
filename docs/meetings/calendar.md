<h1>RCOS Calendar</h1>

<div id="calendar"></div>

<script>
var calendarEl = document.getElementById('calendar');
var calendar = new FullCalendar.Calendar(calendarEl, {
    initialView: 'dayGridMonth',
    timezone: 'America/New_York',
    events: function(info, successCallback, failureCallback) {
        fetch("https://rcos-api.herokuapp.com/api/v1/meetings/")
            .then(res => res.json())
            .then(meetings => {
                successCallback(meetings.map(m => ({
                    title: m.title || "Meeting",
                    start: m.start_date_time + "Z",
                    end: m.end_date_time + "Z",
                })));
            })
            .catch(failureCallback)
    }
});
calendar.render();
</script>