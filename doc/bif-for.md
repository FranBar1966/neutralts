{:for; ... :}
=============

For loop.

```html
{:for; varname from..to >> code :}

{:for; var 1..10 >>
    {:;var:}
:}
```

Modifiers:
----------

```html
{:^for; ... :}
```

No flags
--------

Examples
--------

```html
{:for; n 1..10 >>
    {:;n:}
:}
```

Reverse:

```html
{:for; n 10..1 >>
    {:;n:}
:}
```

---
