{:else; ... :}
==============

Output code if the output of the above bif called is empty (zero length).

```text
{:else; code :}

{:;varname:}{:else; shown if varname is empty :}
```

Modifiers:
----------

```text
{:^else; ... :}
{:!else; ... :}
```
### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

### Modifier: ! (not)

```text
{:;varname:}{:!else; shown if varname is not empty :}
```

No flags
--------

Nesting
-------

Can be nested (no limit):

```text
{:code; ... :}
{:else;
    {:;varname:}{:else; ... :}
:}
```

Grouping:

```text
{:code;
    {:;foor:}
    {:;bar:}
:}{:else;
    foo and bar are empty
:}
```

Can be chained, the following is possible:

```text
{:code;
    {:;foor:}
    {:;bar:}
:}{:else;
    foo and bar are empty
:}{:else;
    {:* if previous "else" is empty *:}
    foo or bar are not empty
:}
```

Usage
-----

Unpredictable results if not immediately after another bif, for example at the beginning of a template. Some bifs always return an empty string, so it doesn't make much sense to add "else" after.

```text
{:moveto; ... :}
{:else; moveto always outputs an empty string :}
```

```text
{:param: ... :}
{:else; param always outputs an empty string :}
```

Regardless of the result of an expression, but the output of the block, in this example it does not matter if varname is defined, but if the block it returns is empty or not:

```text
{:defined; varname >> {:* void *:} :}
{:else;
    The previous block is empty,
    but I don't know what happened to varname
:}
```

For a construction taking into account the result of the expression, you can do this other:

```text
{:defined; varname >> ... :}
{:!defined; varname >> ... :}
```

Only the output of the last bif is relevant, it does not matter if there is something else in between. Next is the same:

```text
{:code;
    {:;foor:}
    {:;bar:}
:}{:else;
    foo and bar are empty
:}
```

```text
{:code;
    {:;foor:}
    {:;bar:}
:}
<div>
    ...
</div>
{:else;
    foo and bar are empty
:}
```

But the second way will be confusing.

---
