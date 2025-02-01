{:replace; ... :}
=================

Replace all occurrences in code part.

```html
{:replace; /from/to/ >> code :}
```

Any delimiter can be used:

```html
{:replace; ~from~to~ >> ... :}
{:replace; ~\~/~ >> ... :}
{:replace; #from#to# >> ... :}
{:replace; |from|to| >> ... :}
{:replace; XfromXtoX >> ... :}
...
```

Modifiers:
----------

```html
{:^replace; ... :}
```

No flags
--------

Example
-------

```html
{:replace; / /_/ >> Hello World :}
```

Output

```html
Hello_World
```

---
