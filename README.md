# Tracker Website - Part of [Tracker project](https://github.com/lchristmann/Tracker)

This project contains the simple website that is part of the "Tracker" Android app's system architecture (see diagram in its repo's README.md).

- the site uses the `locations.json` file as input
- draws a map on the screen (full-screen)
- marks the measurements on the map
  - adds popups with nicely formatted date and time information (your local time zone will be used)
  - the most recent location is highlighted red

## This project's sample data

The sample data contained in the `locations.json` file displays a person that walks up the Lech river in Augsburg

- with 8 measurements taken
- over 2 hours (1 measurement every 15 minutes, from 25th Feb 2025 16:00 to 17:45)

Additionally, there's one measurement in the Siebentischwald forest from 22th Feb 2025, that I used to test the date and time formatting feature.

The [route is approximately this on Google Maps](https://www.google.de/maps/dir/Wolfram+-+Herrenbachviertel,+86163+Augsburg/48.4460278,10.8846667/@48.4008354,10.8214104,23647m/data=!3m2!1e3!4b1!4m9!4m8!1m5!1m1!1s0x479e98265ff31373:0x1eee5d7b82f11944!2m2!1d10.936081!2d48.3554513!1m0!3e2?entry=ttu).

## Technologies chosen

- [Vue 3](https://vuejs.org/) as a frontend (JavaScript) framework
- [Leaflet.js](https://leafletjs.com/) (open-source JavaScript library for mobile-friendly interactive maps)
  - OpenStreetMaps as map provider

Both dependencies are included via CDN links, keeping it as simple as possible.

The whole project is just a `index.html` file (and a `favicon.ico` image resource).

## About the code

The bulk of the site is contained in a 150-line-long `script` tag. In short:

- `<div id="app">` is controlled by the Vue framework
- `<div id="map"></div>` is controlled by the Leaflet.js library
- in the big `script` there is
  - first the Vue app being intialized with `createApp()` -> the main app component is created
  - when it has been created and put into the DOM, the `mounted()` function is run
    - [immediate, synchronous] `initMap()`: sets the map up
    - [asynchronous] `loadLocations()`: fetches the data from `locations.json`, adds markers and
      - uses the `formatDate()` method to display nice dates in the marker popups

## Deployment

The deployment of the website to the target S3 bucket `tracker-website` is automated with a [GitHub Actions](https://github.com/features/actions) CI/CD pipeline.