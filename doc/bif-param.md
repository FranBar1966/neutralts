{:param; ... :}
===============

Set custom parameters, no output in set, output value in get.

```html
{:param; name >> value :} {:* set *:}
{:param; name :}          {:* get *:}
```

Modifiers:
----------

```html
{:^param; ... :}
```

No flags
--------

Usage
-----

The parameters must necessarily be defined within and at the beginning of the bif "code".

```html
{:code;
    {:param; name1 >> value :}
    {:param; name2 >> value :}
    ...
:}
```

The parameters have block scope, will be inherited and recover their value:

```html
{:code;
    {:param; name >> 1 :}
    {:code;
        {:param; name >> 2 :}
    :}
    {:* "name" will recover their value *:}
:}
```

Example of passing arguments to template:

```html
{:code;
    {:param; option >> value :}
    {:include; foo.tpl :}
:}
```

Example of passing arguments to snippet:

```html
{:code;
    {:param; option >> blue :}
    {:snippet; foo :}
:}
```

The snippet may be:

```html
{:snippet; foo >>
    The option is: {:param; option :}
:}
```

---
