{:fetch; ... :}
===============

Perform a JS fetch request.

```text
{:fetch; |url|event|wrapperId|class|id|name| >> code :}
```
Code is the html that will be displayed before performing the `fetch`, it can be a message, a button or the fields of a form.

* url: url to perform fetch, mandatory.
* event: can be; none, form, visible, click, auto, default auto.
* wrapperId: alternative container wrapper ID, default none
* class: add to container class, default none
* id: container ID, default none
* name: container name, default none

The url is the only mandatory parameter:

```text
{:fetch; "/url" >> <div>loading...</div> :}
```

Any delimiter can be used, but a delimiter is always required, even if only one parameter is used.

```text
{:fetch; "url" >> ... :}
{:fetch; ~url~event~ >> ... :}
{:fetch; #url#event# >> ... :}
{:fetch; |url|event| >> ... :}
{:fetch; 'url'event' >> ... :}
...
```

The reason you can use different delimiters is to use one that does not appear in the parameter, using `/` would cause problems with the `url` so we use `"` or any other:

```diff
-{:fetch; //url/ >> ... :} {:* error *:}
+{:fetch; "/url" >> ... :}
```

Modifiers:
----------

```text
{:^fetch; ... :}
```

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)


No flags
--------

event auto
----------

Performs the `fetch` automatically on page load:

```text
{:fetch; |/url|auto| >> <div>loading...</div> :}
```

event none
----------

No event, waiting for you to provide a custom event to perform the `fetch`:

```text
{:fetch; |/url|none| >> ... :}
```

Do not confuse `none` with leaving the parameter empty, leaving it empty would be `auto` by default.

event click
-----------

Perform the `fetch` on click:

```text
{:fetch; |/url|click| >> <button type="button">Click Me!</button> :}
```

event visible
-------------

Performs the `fetch` when the containing element is visible, it can be useful to display content in modals, images or on the scroll:

```text
{:fetch; |/url|visible| >> <div>loading...</div> :}
```

event form
----------

The `form` event generates a form:

```text
{:fetch; |/url|form| >>
    <input type="text" name="paramValue">
    <button type="submit">Send</button>
:}
```

The above will automatically generate HTML similar to this:

```text
<form class="neutral-fetch-form" method="POST" action="/url">
    <input type="text" name="paramValue">
    <button type="submit">Send</button>
</form>
```

And the form will be sent with `fetch` formatting the parameters automatically, even if file uploads are included.

neutral.js
----------

By default when you first call `fetch` the necessary JavaScript script is automatically added to the end of `body`.

This behavior can be changed in `schema` with `disable_js` to `true` for performance reasons:

```text
{
    "config": {
        "disable_js": true
    }
}
```

In this case you will have to manually add to your template at the end of `body` the script:

```text
<html>
    <body>
        ...
        <script src="neutral.min.js"></script>
    </body>
</html>
```

You can download it here: [neutral.min.js](https://gitlab.com/neutralfw/neutralts/-/tree/master/js)

---
