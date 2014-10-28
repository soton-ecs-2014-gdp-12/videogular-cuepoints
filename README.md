videogular-cuepoints
====================

Videogular Cuepoints is a [Videogular](http://videogular.com/) plugin for displaying 'cuepoints', marks on the scrub bar which can be positioned at a particular time. For example, cuepoints could be used to indicate the start of a section in the video, or a time when a pop-up will appear.

Usage
-----

First, import the JavaScript file `cuepoints.js`, then add the dependency `uk.ac.soton.ecs.videogular.plugins.cuepoints` to your Angular project.

Next, add a `<vg-cuepoints>` element as a child of the `<vg-scrubbar>` of your Videogular player. Its `vg-cuepoints-config` attribute should be an object in your parent scope containing the cuepoints (see below), and the `vg-cuepoints-theme` attribute should point to the URL of a CSS file, just like Videogular's [`vg-theme` attribute](https://github.com/2fdevs/videogular/wiki/Themes).

For example, [Videogular's example 2](http://videogular.com/examples/example02.html) with cuepoints added would look like this:

```html
<videogular vg-player-ready="onPlayerReady" vg-theme="config.theme.url">
	<vg-video vg-src="config.sources"></vg-video>

	<vg-controls vg-autohide="config.autoHide" vg-autohide-time="config.autoHideTime">
		<vg-play-pause-button></vg-play-pause-button>
		<vg-timedisplay>{{ API.currentTime | date:'mm:ss' }}</vg-timedisplay>
		<vg-scrubBar>
			<vg-scrubbarcurrenttime></vg-scrubbarcurrenttime>
			<vg-cuepoints vg-cuepoints-config="config.plugins.cuepoints" vg-cuepoints-theme="config.plugins.cuepoints.theme.url"></vg-cuepoints>
		</vg-scrubBar>
		<vg-timedisplay>{{ API.timeLeft | date:'mm:ss' }}</vg-timedisplay>
		<vg-volume>
			<vg-mutebutton></vg-mutebutton>
			<vg-volumebar></vg-volumebar>
		</vg-volume>
		<vg-fullscreenButton></vg-fullscreenButton>
	</vg-controls>
</videogular>
```

With the following added to your `$scope.config` object:

```js
plugins: {
	cuepoints: {
		theme: {
			url: "lib/videogular-cuepoints/cuepoints.css",
				// Replace with the path appropriate to your project
		},
		points: [
			{ time:  18 },
			{ time: 100 },
		],
	},
},
```

Styling cuepoints
-----------------

Each cuepoint is a `<vg-cuepoint>` element, and can be styled accordingly. You can see how they're styled by default in `cuepoints.css`. For example, if you wanted to change the color of the cuepoints to blue, you might write the following in your CSS file:

```css
videogular vg-cuepoints vg-cuepoint {
	background-color: blue;
}
```

You should be able to change any CSS properties without causing problems, except `position`. (`left` can be set but will always be overridden when the cuepoint is positioned.)
