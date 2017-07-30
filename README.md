[![NPM][npm-badge-img]][npm-badge-link]
[![Code Climate][codeclimate-badge]][codeclimate-url]
[![Coverage Status][coverage-badge]][coverage-url]
[![Ember Observer Score][ember-observer-badge]][ember-observer-url]

# ember-cli-bodymovin

A little wrapper for [Bodymovin](https://github.com/bodymovin/bodymovin), an After Effects plugin for exporting animations to svg/canvas/html + js.

## Installation

`ember install ember-cli-bodymovin`

## Usage

Rendering your animation out of AE using the [bodymovin extension](https://github.com/bodymovin/bodymovin#installing-extension-finally-the-plugin-is-on-the-adobe-add-ons) will generate a `json` representation of your animation. COol.

Grab that puppy and drop it into your app's public dir `public/animations/coolFileName.json`. Then all you need to do is drop that sucker onto the page:

##### Basic usage
`{{body-movin path='coolFileName'}}`

##### External Files

Sometimes you may need or want to host your animation json somewhere else. No problem, just set `external=true` and include the full path.
```
{{body-movin
	path='//lab.nearpod.com/bodymovin/demo/pancakes/data.json'
	external=true}}
```

## Interacting with your animation
You can use any of the Bodymovin.js primitives in your Component/Controller. [Check them out](https://github.com/bodymovin/bodymovin#usage).

```hbs
{{!-- templates/component/playPause-animation.hbs --}}

{{body-movin
	path='reel'
	setup=(action setup)
	click=(action toggle)
	}}

```

```javascript
// component/playPause-animation.js

import Ember from 'ember';

export default Ember.Component.extend({
  animation: null,
  state: {
    playing: true
  },

  actions: {
    setup(data) {
      this.set('animation', data);
    },

    toggle() {
      let state = this.get('state');
      let animation = this.get('animation');

      if (state.playing) {
        animation.pause();
        this.set('state.playing', false);
      } else {
        animation.play();
        this.set('state.playing', true);
      }
    }

  }

});

```


## Options
You can override all the default stuff as you'd expect.

```
{{body-movin
	path='loading'
	renderStyle='canvas'
	autoplay=false
	autorender=true
	rendererSettings=myRendererSettings
	click=(action 'submit') // Handle in your component/controller
	setup=(action 'mySetup') // Handle in your component/controller
}}
```

#### animation (String)
The file name OR url of your animation.

#### external (Boolean)
Set this to true if you're including an external source as your `path`.

#### renderType (String)
Set to 'svg' / 'canvas' / 'html' to set the renderer. If you leave it of, we'll default to our favorite- `SVG`.

#### rendererSettings (Object)
Some additional renderer settings for max control.
```
rendererSettings: {
  context: canvasContext, // the canvas context
  scaleMode: 'noScale',
  clearCanvas: false,
  progressiveLoad: false, // Boolean, only svg renderer, loads dom elements when needed. Might speed up initialization for large number of elements.
  hideOnTransparent: true //Boolean, only svg renderer, hides elements when opacity reaches 0 (defaults to true)
}
```


#### loop (String)
true / false / number

#### autoplay (Boolean)
true / false


# Contributing

Hook it up!

## Running

* `ember serve`
* Visit your app at [http://localhost:4200](http://localhost:4200).

## Running Tests

* `npm test` (Runs `ember try:each` to test your addon against multiple Ember versions)
* `ember test`
* `ember test --server`

## Building

* `ember build`

For more information on using ember-cli, visit [http://ember-cli.com/](http://ember-cli.com/).


[npm-badge-img]: https://badge.fury.io/js/ember-cli-bodymovin.svg
[npm-badge-link]: http://badge.fury.io/js/ember-cli-bodymovin
[ember-observer-badge]: http://emberobserver.com/badges/ember-cli-bodymovin.svg
[ember-observer-url]: http://emberobserver.com/addons/ember-cli-bodymovin
[codeclimate-badge]: https://codeclimate.com/github/jakeleboeuf/ember-cli-bodymovin/badges/gpa.svg
[codeclimate-url]: https://codeclimate.com/github/jakeleboeuf/ember-cli-bodymovin
[coverage-badge]: https://codeclimate.com/github/jakeleboeuf/ember-cli-bodymovin/badges/coverage.svg
[coverage-url]: https://codeclimate.com/github/jakeleboeuf/ember-cli-bodymovin/coverage