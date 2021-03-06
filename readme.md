# wait-element
[![Travis (.org)](https://img.shields.io/travis/1natsu172/wait-element.svg?style=for-the-badge)](https://travis-ci.org/1natsu172/wait-element)
[![npm](https://img.shields.io/npm/v/@1natsu/wait-element.svg?style=for-the-badge)](https://www.npmjs.com/package/@1natsu/wait-element)
![npm bundle size (minified)](https://img.shields.io/bundlephobia/min/@1natsu/wait-element.svg?style=for-the-badge)
![npm bundle size (minified + gzip)](https://img.shields.io/bundlephobia/minzip/@1natsu/wait-element.svg?style=for-the-badge)


> Detect the appearance of an element in the browser DOM

## a.k.a promise-querySelector

* Promise API
* Driven by `MutationObserver`
* Detect by `querySelecrtor`

If the target element already exists when execution of "wait-element", it immediately `resolve` and return the element.


## Install

```bash
$ npm install @1natsu/wait-element
```

## Usage

### Module specifiers

```js
// ES
import waitElement from '@1natsu/wait-element';

// CJS
const waitElement = require('@1natsu/wait-element');
// In some cases this
const waitElement = require('@1natsu/wait-element').default;
```

#### Basically

```js
(async () => {
  const el = await waitElement('.late-comming');
  console.log(el);
  //=> example: "<div class="late-comming">I'm late</div>"
})();
```

#### When specify a parent element (specify MutationObserve target)

```js
(async () => {
  const parent = await waitElement('#parent');
  const el = await waitElement('.late-comming', { target: parent });
  console.log(el);
  //=> example: "<div class="late-comming">I'm late</div>"
})();
```

#### When setting timeout

```js
(async () => {
  const el = await waitElement('.late-comming', { timeout: 5000 }).catch(err => console.log(err));
  console.log(el);
  //=> If detected element: "<div class="late-comming">I'm late</div>"
  //=> If timeouted: Error: Element was not found: '.late-coming'
})();
```

#### When cancel wait-element

```js
(async () => {
  let el;

  try {
    el = waitElement('.late-comming');
    if (!isCondition) el.cancel();
  } catch {
    // some handling...
  }
})();
```


## API

### waitElement(selector, [options])

#### selector

Type: `string`

Format is [CSS-selector](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Selectors)

#### options

##### target

Type: `HTMLElement`<br>
Default: `document`

Specify a parent node (specify MutationObserve target).

When you know the parent node of the element you want to detect.

* Please also refer to the [MutationObserver](https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver)

##### timeout

Type: `number`<br>
Default: `0`<br>
Unit: ms(Millisecond)

There is no timeout by default.

### waitElementPromise#cancel()
Type: `Function`

Stop waiting for the element. Cancellation is synchronous.

Based on [p-cancelable](https://github.com/sindresorhus/p-cancelable). Appreciate it.

## Similar

The very similar library.

* [element-ready](https://github.com/sindresorhus/element-ready)
  * Implementation method is different from this library.


## License

MIT © [1natsu172](https://github.com/1natsu172)
