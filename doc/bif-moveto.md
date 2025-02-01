{:moveto; ... :}
================

Move the code to the specified tag, no output. The code is parsed before moving.

```html
{:moveto; tagname >> code :}

{:moveto; <tag >> ... :}
{:moveto; </tag >> ... :}
```

Moves to the inside of the tag, at the beginning or at the end depending on whether the slash is included.

Note that it is designed to move libraries, js, css, etc, not to arbitrarily move code to any tag, if it moves to a "div" it will do it to the first one it finds.

Custom tags can be created to mark the places where certain code should be moved.

Modifiers:
----------

```html
{:^moveto; ... :}
```

No flags
--------

Usage
-----

An ID is generated with the code to be moved, so that the same code is only moved once. The following will only move once even if it is quoted several times throughout the app:

```html
{:moveto; </head >> <script src="jquery.min.js"></script> :}
{:moveto; </head >> <script src="jquery.min.js"></script> :}
```

Since this is the desired behavior, so that the code is always the same, it is better to create snippets:

```html
{:snippet; include-jquery >>
    <script src="jquery.min.js"></script>
:}

{:moveto; </head >> {:snippet; include-jquery :} :}
```

Or:

```html
{:snippet; include-jquery >>
    {:moveto; </head >> <script src="jquery.min.js"></script> :}
:}

{:snippet; include-jquery :}
```

Example:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
    </head>
    <body>
        <script src="jquery.min.js"></script>
    </body>
</html>

{:moveto; </head >> <meta name="meta" content="anything"> :}
{:moveto; <body  >> <script> // script 1 </script> :} {:* move to start body *:}
{:moveto; </body >> <script> // script 2 </script> :} {:* move to end body *:}
```

Result:

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="meta" content="anything">
    </head>
    <body>
        <script> // script 1 </script>
        <script src="jquery.min.js"></script>
        <script> // script 2 </script>
    </body>
</html>
```

---