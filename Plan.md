# App Idea outline

## Features and functionality
- Be able to set Alarm
  - Set a re-occurring alarm for each day of the week
  - Set multiple alarm and turn them off and on
  - Delete individual alarms
  - Set snooze (snooze time)
  - Change alarm sound for each alarm

- See the weather
  - Weather for today in detail
  - 5 Day forecast
  - Set by current location as default
  - Have multiple __pages__ of weather for different locations
  - Set temperature type between Fahrenheit and Celsius

- Have main page for landscape with weather and agenda side by side (split screen style)
- When alarm goes off and is dismissed have Android TTS announce weather and first item on agenda/when to leave for work (if possible)
- Have each feature adjustable and toggle on and off
- Aim to have portrait style with each aspect on a different page, swipe side to side to or tap list at the top to change between each function.

### Order of priority

1. Weather - Have weather app with current and 5 day forecast and the ability to change direction and temp type.
2. An Alarm app - with all the features outlined above.
3. Improve the weather app to use TTS and say the weather for the day (Like google now does).
4. Integrate weather and alarm.
5. Integrate basic calender function - Display calender and open app
6. Show agenda and link with google maps for travel time (if possible).

## Simple Actions for __Basic__ Weather

1. When the app opens it will receive the users location from sensors
  * Include location permissions into manifest
  * Store location as a variable
  * Convert location data into (long, lat) to WOEID

    YQL = ```YQL SELECT * FROM geo.places WHERE text="{$seedLat}, {$seedLong}" AND placeTypeName.code = 7```

    REST = ```REST http://query.yahooapis.com/v1/public/yql?q=SELECT%20*%20FROM%20geo.places%20WHERE%20text%3D%22{$seedLat}%2C%20{$seedLong}%22%20AND%20placeTypeName.code%20%3D%207&format=json&diagnostics=true&callback=```

2. Pull data from Yahoo weather api using user location
3. Parse JSON data retrieved from Yahoo
  * Deal with failure - Display snackbar/dialog to inform of failure, "ERROR, try again later"
  * On success continue to run app.
4. With data parsed display output using imageViews (Current condition, 5 day forecast) and textViews for current condition, temp, location, any other relevant data.
  * Use relative layout for current weather.
  * Use listArray for 5-day forecast - LinearLayout Vertical
5. Set refresh rate - Every 30 minutes? (Make adjustable by user between 15 mins - 24 hours)

## Simple Actions for Alarm

1. Display list of alarms - ListArray of alarm objects
2. Have a floating button to add alarms at the bottom
3. When creating alarm use floating time picker
4. On alarm creation expand new alarm settings to allow for settings
  * Repeat
  * Ringtone
  * Label
  * Vibrate
  * DELETE
5. Option to toggle alarm on and off will always be visible
6. On deletion display snackbar informing of deletion and allow for undo

## Simple actions for Improved Weather

1. Allow user to change location
 * Populate a list of locations or provide suggestions for location as user types? (Not sure how to do either).
2. Have each location as a weather object
  * Location
  * Current weather condition
  * Current temp
  * 5-day forecast
3. Implement a button to add a new location
4. New button to speak the current weather.
  * Example: The weather in $location is currently $condition and is $temperature degrees $metric/imperial.
5. Use a switch statement to add extra comment. See activity diagram Weather.png
