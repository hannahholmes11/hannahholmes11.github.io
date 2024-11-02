<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weekly Events Summary</title>
    <style>
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
        const calendarId = '8410a6a2350f9164a421f17e230325dddfd9588dcd47612f57a0541d07575008@group.calendar.google.com'; // Replace with your actual Calendar ID
        const apiKey = 'AIzaSyBrZ9Q078IvTAQCg17WUo57_JwJlE9Xdt0'; // Replace with your actual API Key

        // Fetch events from Google Calendar API
        try {
            const response = await fetch(`https://www.googleapis.com/calendar/v3/calendars/${8410a6a2350f9164a421f17e230325dddfd9588dcd47612f57a0541d07575008}/events?key=${AIzaSyBrZ9Q078IvTAQCg17WUo57_JwJlE9Xdt0}`);
            const data = await response.json();
            
            // Check if the response has items
            if (data.items && data.items.length > 0) {
                const eventList = document.getElementById('eventList');
                eventList.innerHTML = ''; // Clear any previous contents

                // Display each event in the widget
                data.items.forEach(event => {
                    const listItem = document.createElement('li');
                    listItem.className = 'event-item';
                    listItem.innerHTML = `
                        <div><strong>${event.summary || 'No Title'}</strong></div>
                        <div class="event-time">${new Date(event.start.dateTime || event.start.date).toLocaleString()}</div>
                    `;
                    eventList.appendChild(listItem);
                });
            } else {
                console.error('No events found or an error occurred:', data);
                document.getElementById('eventList').innerHTML = 'No events found for this week.';
            }
        } catch (error) {
            console.error('Error loading events:', error);
            document.getElementById('eventList').innerHTML = 'Failed to load events.';
        }
    }

    // Run the function to fetch and display events
    fetchGoogleCalendarEvents();
</script>

</body>
</html>
