{:else; ... :}
==============

Output code if the output of the above bif called is empty (zero length).

```textplain
{:else; code :}

{:;varname:}{:else; shown if varname is empty :}
```

Modifiers:
----------

```textplain
{:^else; ... :}
{:!else; ... :}
```

### Modifier: ! (not)

```textplain
{:;varname:}{:!else; shown if varname is not empty :}
```

No flags
--------

Nesting
-------

Can be nested (no limit):

```textplain
{:code; ... :}
{:else;
    {:;varname:}{:else; ... :}
:}
```

Grouping:

```textplain
{:code;
    {:;foor:}
    {:;bar:}
:}{:else;
    foo and bar are empty
:}
```

Can be chained, the following is possible:

```textplain
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

```textplain
{:moveto; ... :}
{:else; moveto always outputs an empty string :}
```

```textplain
{:param: ... :}
{:else; param always outputs an empty string :}
```

Regardless of the result of an expression, but the output of the block, in this example it does not matter if varname is defined, but if the block it returns is empty or not:

```textplain
{:defined; varname >> {:* void *:} :}
{:else;
    The previous block is empty,
    but I don't know what happened to varname
:}
```

For a construction taking into account the result of the expression, you can do this other:

```textplain
{:defined; varname >> ... :}
{:!defined; varname >> ... :}
```

Only the output of the last bif is relevant, it does not matter if there is something else in between. Next is the same:

```textplain
{:code;
    {:;foor:}
    {:;bar:}
:}{:else;
    foo and bar are empty
:}
```

```textplain
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