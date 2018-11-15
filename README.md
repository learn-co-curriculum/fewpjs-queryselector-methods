# JavaScript Node Search Power Tools

## Learning Goals

1. Use `document.querySelector()` and `document.querySelectorAll()` to find nested nodes
2. Change value of targeted DOM nodes

## Introduction

One of the most essential skills in our web development toolbox is finding
elements in the DOM.

While `document.getElementById()` and `document.getElementsByClassName()` are
good, we can improve our search when we use document structure (tag, `id`, `class`) **and** the tree structure of the DOM.

To practice finding elements in the DOM, we're going to make use of two methods that are useful for navigating the DOM: `document.querySelector()` and
`document.querySelectorAll()`.

## Use `document.querySelector()` and `document.querySelectorAll()` to find nested nodes

### `querySelector()`

`querySelector()` takes one argument, a string of [selectors][], and returns
the first element that matches these selectors.

Given a document like

``` html
<body>
  <div>
    Hello!
  </div>

  <div>
    Goodbye!
  </div>
</body>
```

If we called `document.querySelector('div')`, the method would return the first
`div` (whose content is "Hello!").

Selectors aren't limited to one tag name, though (otherwise why not just use
`document.getElementsByTagName('div')[0]`?). We can get very specific.

``` html
<body>
  <div>
    <ul class="ranked-list">
      <li>1</li>
      <li>
        <div>
          <ul>
            <li>2</li>
          </ul>
        </div>
      </li>
      <li>3</li>
    </ul>
  </div>

  <div>
    <ul class="unranked-list">
      <li>6</li>
      <li>2</li>
      <li>
        <div>4</div>
      </li>
    </ul>
  </div>
</body>
```

```javascript

// get <li>2</li>
const li2 = document.querySelector('ul.ranked-list li ul li')

// get <div>4</div>
const div4 = document.querySelector('ul.unranked-list li div')

```

In the above example, the first query says, "Starting from `document` (the
object we've called `querySelector()` on), find a `ul` with a `className` of
`ranked-list` (the `.` is for `className`).

Then find an `li` that is a child of that `ul`. Then find a `ul` that is a
child (but not necessarily a direct descendant) of that `li`. Finally, find an
`li` that is a child of that (second) `ul`."

**NOTE:** The HTML property `class` is referred to as `className` in JavaScript. It's mildly confusing, but we can memorize it and get past it with enough time.

What, then, does the second call to `querySelector()` say? Puzzle it out for a
bit, and then read on.

Wait for it...

Okay, the second call says, "Starting from `document`, find a `ul` with a
`className` of `unranked-list`. Then find an `li` descended from `ul.unranked-
list` and a `div` descended from that `li`."

#### CSS Selectors

Remember selectors? Now is probably a good time to brush up on [selectors][]. Play
around on the MDN page, then come back when you're ready.

### `querySelectorAll()`

`querySelectorAll` works a lot like `querySelector()` — it accepts a selector
as its argument, and it searches starting from the element that it's called on
(or from `document`) — but instead of returning the first match, it returns a
`NodeList` (which, remember, is not an `Array`) of all matching elements.

Given a document like

``` html
<main id="app">
  <ul class="ranked-list">
    <li>1</li>
    <li>2</li>
  </ul>

  <ul class="ranked-list">
    <li>10</li>
    <li>11</li>
  </ul>
</main>
```

If we called `document.getElementById('app').querySelectorAll('ul.ranked-list li')`, we'd get back a list of Nodes corresponding to: `<li>1</li>, <li>2</li>, <li>10</li>, <li>11</li>`.


## Conclusion

The DOM selection methods `document.querySelector()` and
`document.querySelectorAll()` are powerful tools for finding elements we need
to update and change. 


## Resources

- [document.querySelector()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)
- [document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)

[selectors]: https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_Started/Selectors
