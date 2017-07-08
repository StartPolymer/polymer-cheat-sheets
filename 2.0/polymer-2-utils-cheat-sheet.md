# Polymer 2.0 Utils Cheat Sheet

> Utility APIs for Polymer 2.0 library.

Docs: [Common utility APIs](https://www.polymer-project.org/2.0/docs/upgrade#common-utility-apis)

## Async

```html
<link rel="import" href="/bower_components/polymer/lib/utils/async.html">
```

```js
// in JS, execute someMethod with microtask timing
Polymer.Async.microtask.run(() => this.someMethod());
```

For async with a timeout use native `setTimeout`:

```js
setTimeout(() => this.someMethod(), 500);
```

## Debounce

```html
<link rel="import" href="/bower_components/polymer/lib/utils/debounce.html">
```

```js
this._debouncer = Polymer.Debouncer.debounce(this._debouncer,
    Polymer.Async.timeOut.after(250),
    () => { this.doSomething() });
```

## Fire

Instead of using the legacy
`this.fire('some-event')` API, use the equivalent platform APIs:

```js
this.dispatchEvent(new CustomEvent('some-event', { bubbles: true, composed: true }));
```

The `fire` method sets the `bubbles` and `composed` properties by default. For more on using custom
events, see [Fire custom events](/{{{polymer_version_dir}}}/docs/devguide/events#custom-events).

(The `CustomEvent` constructor is not supported on IE, but the webcomponents polyfills include a
small polyfill for it so you can use the same syntax everywhere.)

## importHref

```js
Polymer.importHref(this.resolveUrl('some-other-file.html'),
    () => this.onLoad(loadEvent),
    () => this.onError(errorEvent),
    true /* true for async */);
```

## Using the legacy APIs

If you want to upgrade to a class-based element but depend on some of the removed APIs, you can
add most of the legacy APIs by using the `LegacyElementMixin`.

```js
class MyLegacyElement extends Polymer.LegacyElementMixin(Polymer.Element) { ... }
```

[Mixin Polymer.LegacyElementMixin](https://www.webcomponents.org/element/Polymer/polymer/mixins/Polymer.LegacyElementMixin)
