<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weekly Events Summary</title>
    <style>
        /* CSS for styling the widget */
        .widget-container {
            width: 100%;
            max-width: 400px;
            font-family: Arial, sans-serif;
            background-color: #ffffff;
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        .widget-header {
            font-size: 18px;
            font-weight: bold;
            margin-bottom: 10px;
            text-align: center;
        }
        .event-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }
        .event-item {
            margin-bottom: 12px;
            border-bottom: 1px solid #f0f0f0;
            padding-bottom: 8px;
        }
        .event-time {
            color: #888;
            font-size: 12px;
        }
    </style>
</head>
<body>

<div class="widget-container">
    <div class="widget-header">This Week's Events</div>
    <ul class="event-list" id="eventList"></ul>
</div>

<script>
   async function fetchGoogleCalendarEvents() {
        // Replace 'YOUR_CALENDAR_ID' with your actual Calendar ID found in Google Calendar settings
        const calendarId = 'hannah.h.holmes@gmail.com'; // Replace this with your actual Calendar ID
        const apiKey = 'AIzaSyBrZ9Q078IvTAQCg17WUo57_JwJlE9Xdt0';

        // Fetch events from Google Calendar API
        const response = await fetch(`https://www.googleapis.com/calendar/v3/calendars/${hannah.h.holmes@gmail.com}/events?key=${apiKey}`);
        const data = await response.json();

        // Format the event data to display title and start time
        return data.items.map(event => ({
            title: event.summary,
            time: new Date(event.start.dateTime || event.start.date).toLocaleString(),
            source: 'Google Calendar'
        }));
    }

    async function displayEvents() {
        const eventList = document.getElementById('eventList');
        eventList.innerHTML = 'Loading events...';

        try {
            // Fetch events from Google Calendar only
            const googleEvents = await fetchGoogleCalendarEvents();

            // Sort events by time
            const sortedEvents = googleEvents.sort((a, b) => new Date(a.time) - new Date(b.time));

            // Display events in the widget
            eventList.innerHTML = '';
            sortedEvents.forEach(event => {
                const listItem = document.createElement('li');
                listItem.className = 'event-item';
                listItem.innerHTML = `
                    <div><strong>${event.title}</strong></div>
                    <div class="event-time">${event.time}</div>
                `;
                eventList.appendChild(listItem);
            });
        } catch (error) {
            console.error('Error loading events:', error);
            eventList.innerHTML = 'Failed to load events.';
        }
    }

    displayEvents();
</script>

</body>
</html>

