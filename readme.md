# Swup Scroll plugin

## Instalation
This plugin can be installed with npm

```bash
npm install @daun/swup-scroll-plugin
```

and included with import

```shell
import SwupScrollPlugin from '@daun/swup-scroll-plugin';
```

or included from the dist folder

```html
<script src="./dist/SwupScrollPlugin.js"></script>
```

## Usage

To run this plugin, include an instance in the swup options.

```javascript
const swup = new Swup({
  plugins: [new SwupScrollPlugin()]
});
```

## Options
### animateScrollBetweenPages
`animateScrollBetweenPages` defines whether the scroll animation is enabled between page visits or swup simply sets the scroll without animation instead.

### animateScrollOnSamePage
`animateScrollOnSamePage` defines whether the scroll animation is enabled for anchor scrolls on the same page or swup simply sets the scroll without animation instead.

### doScrollingRightAway
`doScrollingRightAway` defines if swup is supposed to wait for the replace of the page to scroll to the top. Only makes a difference if `animateScrollBetweenPages` is `true`.

### scrollFriction and scrollAcceleration
Animation of scroll is adjustable with options `scrollFriction` and `scrollAcceleration`.

### findTarget
Customize how the scroll target is found on the page. Defaults to looking for matching `id` attributes.

```javascript
{
  // Use the `name` attribute instead of `id`
  findTarget: hash => {
    const name = hash.replace('#', '')
    return document.querySelector(`[name="${name}"]`)
  }
}
```

### offset
Offset to substract from the final scroll position, to account for fixed headers. Can be either a number or a function that returns the offset.

```javascript
{
  // Number: fixed offset in px
  offset: 30,

  // Function: calculate offset before scrolling
  offset: () => document.querySelector('#header').offsetHeight,

  // The scroll target element is passed into the function
  offset: target => target.offsetHeight * 2,
}
```

### default options
```javascript
new SwupScrollPlugin({
    doScrollingRightAway: false,
    animateScroll: true,
    scrollFriction: 0.3,
    scrollAcceleration: 0.04,
    offset: 0,
});
```

## Changes of swup instance
Plugins ads `scrollTo` method to the swup instance, which can be later used for custom scrolling.
Method accepts offset in pixels or element you want to scroll to.

Plugin also adds `scrollStart` and `scrollDone` events to swup, that can be listened to with `on` method.
