{:coalesce; ... :}
==================

Output the first non-empty (non-zero length) of a *block* list. Nothing may be displayed if all blocks are empty.

```html
{:coalesce;
    {:;varname1:}
    {:;varname2:}
    {:;varname3:}
:}

{:coalesce;
    {:code;
        {:code; ... :}
        {:code; ... :}
        {:code; ... :}
    :}
    {:code;
        {:code; ... :}
    :}
    {:;varname:}
:}
```

Modifiers:
----------

```html
{:+coalesce; varname >> ... :}
{:^coalesce; varname >> ... :}
```

For more details about the "+" modifier see "modifiers".

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

No flags
--------

Nesting
-------

Can be nested (no limit):

```html
{:coalesce;
    {:coalesce;
        {:code; ... :}
        {:code; ... :}
        {:code; ... :}
    :}
    {:code;
        {:code; ... :}
    :}
:}
```

Blocks
------

Each *block* can be a single Bif, or a nested set of them:

```html
                {:coalesce;
              .---- {:code;
              |         {:code; ... :}
    Block --> |         {:code; ... :}
              |         {:code; ... :}
              `---- :}
              .---- {:code;
    Block --> |         {:code; ... :}
              `---- :}
    Block --------> {:;varname:}
                :}
```

Spaces
------

A variable with spaces is not a zero length string, the following example will show the contents of spaces:

```html
{:coalesce;
    {:;spaces:}
    {:code;
        Hello
    :}
:}
```

In reality, spaces will not be displayed, the output will be empty, since the default behavior of **neutral** is to ignore spaces.

If the variable with spaces was nested, then the result would be an empty block, the following will show "Hello":

```html
{:coalesce;
    {:code;
        {:;spaces:}
    :}
    {:code;
        Hello
    :}
:}
```

Unprintable Bif {:;:} is not a zero length string, the following will show nothing:

```html
{:coalesce;
    {:code;
        {:;:}
    :}
    {:code;
        Hello
    :}
:}
```

Do not show anything if a condition is given:

```html
{:coalesce;
    {:defined; varname >>
        {:;:}
    :}
    {:code;
        Hello
    :}
:}
```

---
