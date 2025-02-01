{:snippet; ... :}
=================

Output or set snippet.

```html
{:snippet; name >> ... :} {:* set  *:}
{:snippet; name :}        {:* play *:}
```

You can use the alias "snip", this is the same:

```html
{:snip; name >> ... :} {:* set  *:}
{:snip; name :}        {:* play *:}
```

Note that snippet, although they can be called anywhere, **must be defined in a file whose name contains the word "snippet".** An error will occur if an attempt is made to define it elsewhere.

Modifiers:
----------

```html
{:^snippet; ... :}
```

Flags
-----

```html
{:snippet; {:flg; static :} ... >> ... :}
```

### Flag: static

By default the content of the snippet is parsed when called, with “static” it is parsed when set.

```html
{:snippet; {:flg; static :} snippet-name >>
    {:;varname:}
:}
```

Therefore, it only works on set.

Usage
-----

The snippet is something like a function, parts of code that you can refer and can contain anything.

Set snippet, no output:

```html
{:snippet; snippet-name >>
    Hello World
:}
```

Play snippet;

```html
{:snippet; snippet-name :}
```

Output:

```html
Hello World
```

---
