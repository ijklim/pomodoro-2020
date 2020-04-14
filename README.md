# Timer for Pomodoro Technique, 2020

Built using Vue.js 2.6.11 with PWA (Progressive Web Apps) and Bootstrap 4.4.1.

<p align="center">
  <a href="https://pomodoro.ivan-lim.com" target="_blank">
    <img src="https://github.com/ijklim/pomodoro-2020/blob/master/public/img/screenshot.jpg" width="990px">
    <br>
    Live Demo
  </a>
</p>

## Technologies/Modules used

* Vue.js
* Vue Router
* Vuex
* Bootstrap (css only)
* Bootstrap Vue

## Features

* 25 minutes Pomodoro interval
* 5 minutes Short Break interval
* 20 minutes Long Break interval
* Different timer text color during break time
* Toggle Sound
* Toggle Autostart Next Interval
* Intervals completed log
* Responsive

## Query string configurations
Function | Parameter | Default | Setting
-------- | --------- | ------- | -------
Whether to start next interval when the current one is completed | autonext | off | on/off
Start timer immediately | autostart | off | on/off
Play sound when the current interval is completed | sound | on | on/off

Example: https://pomodoro.ivan-lim.com?autonext=on&autostart=on&sound=off


## Usage Tip

To open this app in a small window on a desktop machine, type the following into the browser address bar or create a bookmark:
**javascript:window.open('https://pomodoro.ivan-lim.com', 'pomodoro', 'height=350,width=400')**

Note #1: Sometimes browser will skip the front **javascript:** during paste, type this in manually if necessary.

Note #2: Some browsers might not support all the features if invoked this way. For example Microsoft Edge does not support window sizing.


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
