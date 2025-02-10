# Expo Linking.addEventListener Inconsistent Behavior on Cold Start

This repository demonstrates a bug where `Linking.addEventListener` from Expo's Linking API does not consistently fire when the app is launched from a cold start.  Deep links are not properly handled until a subsequent action is performed within the app (like navigating to a new screen).

## Bug Description
The `Linking.addEventListener` method is intended to listen for incoming URLs.  However, in the case of a cold start, it might fail to trigger upon initial launch, thus missing the initial deep link. This behavior is inconsistent and makes reliable handling of deep links challenging.

## Reproduction Steps
1. Clone this repository.
2. Run the app using `expo start`. 
3. Open a new tab and navigate to a deep link URL that the app is configured to handle (as defined in `app.json` and the code).
4. Note that if this is the first time launching the app, the console log in `App.js` will not show the received URL.
5. Navigate to a different screen within the app or perform some user interaction.
6. You will now see the received URL in the console, even if it was sent during the cold start. 

## Solution
See `bugSolution.js` for a possible workaround that involves checking for initial URLs upon app mounting and handling them synchronously.