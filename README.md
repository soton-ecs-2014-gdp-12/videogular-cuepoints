videogular-cuepoints
====================

Videogular Cuepoints is a [Videogular](http://videogular.com/) plugin for displaying 'cuepoints', marks on the scrub bar which can be positioned at a particular time. For example, cuepoints could be used to **indicate** the start of a section in the video, or a time when a pop-up will appear.

**Not to be confused with ["Videogular Cue Points"](http://www.videogular.com/tutorials/videogular-cue-points-synchronize-video-with-twitter/)**, a completely different feature of Videogular implemented long after the release of this plugin.

Installation
------------

Videogular Cuepoints can be installed with Bower:

```
bower install videogular-cuepoints
```

Usage
-----

First, import the JavaScript file `cuepoints.js`, then add the dependency `uk.ac.soton.ecs.videogular.plugins.cuepoints` to your Angular project.

Next, add a `<vg-cuepoints>` element as a child of the `<vg-scrubbar>` of your Videogular player. Its `vg-cuepoints-config` attribute should be an object in your parent scope containing the cuepoints (see below), and the `vg-cuepoints-theme` attribute should point to the URL of a CSS file, just like Videogular's [`vg-theme` attribute](https://github.com/2fdevs/videogular/wiki/Themes).

For example, [Videogular's example 2](http://www.videogular.com/examples/controls-plugin/) with cuepoints added would look like this:

```html
...
<videogular vg-theme="controller.config.theme.url">
	<vg-media vg-src="controller.config.sources"
			  vg-tracks="controller.config.tracks">
	</vg-media>

	<vg-controls vg-autohide="controller.config.plugins.controls.autoHide" vg-autohide-time="controller.config.plugins.controls.autoHideTime">
		<vg-play-pause-button></vg-play-pause-button>
		<vg-time-display>{{ currentTime | date:'mm:ss' }}</vg-time-display>
		<vg-scrub-bar>
			<vg-scrub-bar-current-time></vg-scrub-bar-current-time>
			<vg-cuepoints vg-cuepoints-config="controller.config.plugins.cuepoints"
						  vg-cuepoints-theme="controller.config.plugins.cuepoints.theme.url">
			</vg-cuepoints>
		</vg-scrub-bar>
		<vg-time-display>{{ timeLeft | date:'mm:ss' }}</vg-time-display>
		<vg-time-display>{{ totalTime | date:'mm:ss' }}</vg-time-display>
		<vg-volume>
			<vg-mute-button></vg-mute-button>
			<vg-volume-bar></vg-volume-bar>
		</vg-volume>
		<vg-playback-button></vg-playback-button>
		<vg-fullscreen-button></vg-fullscreen-button>
	</vg-controls>
</videogular>
...
```

With the following added to your `$scope.config` object:

```js
plugins: {
	cuepoints: {
		theme: {
			url: "bower_components/videogular-cuepoints/cuepoints.css",
				// Replace with the path appropriate to your project
		},
		points: [
			{ time: 18 },
			{ time: 60 },
		],
	},
},
```

[A complete example can be found here.][example]

Styling cuepoints
-----------------

Each cuepoint is a `<vg-cuepoint>` element, and can be styled accordingly. You can see how they're styled by default in `cuepoints.css`. For example, if you wanted to change the color of the cuepoints to blue, you might write the following in your CSS file:

```css
videogular vg-cuepoints vg-cuepoint {
	background-color: blue;
}
```

You should be able to change any CSS properties without causing problems, except `position`. (`left` can be set but will always be overridden when the cuepoint is positioned.)

[example]: https://github.com/HarryCutts/videogular-cuepoints-example
