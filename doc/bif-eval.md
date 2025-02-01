{:eval; ... :}
==============

Output code if the result of eval is not empty (non-zero length).

```html
{:eval; code >> code :}

{:eval; {:;varname:} >>
    shown if varname is not empty
:}
```

A variable is set with the result of the evaluation:

```html
{:eval; {:;varname:} >>
    ...
    {:;__eval__:}
    ...
:}
```

Modifiers:
----------

```html
{:!eval; ... :}
{:+eval; ... :}
{:^eval; ... :}
```

For more details about the "+" modifier see "modifiers".

### Modifier: ! (not)

```html
{:!eval; {:;varname:} >>
    shown if varname is empty
:}
```

No flags
--------

Usage
-----

Eval evaluates code versus filled which evaluates a variable:

```html
    {:filled; varname >>
        ...
    :}

    {:eval; {:code: {:;varname:} :} >>
        ...
    :}
```

Sometimes it is necessary to evaluate code:

```html
<li>{:snippet; snippet-name :}</li>
```

The output of the above if "snippet-name" is empty will be:

```html
<li></li>
```

To prevent this from happening, it can be done:

```html
{:eval; {:snippet; snippet-name :} >>
    <li>{:;__eval__:}</li>
:}
```

And in this case the "li" will only be displayed if "snippet-name" is not empty.

The following are equivalent, but the first does not require re-evaluation of the snippet and may be clearer as to what is intended:

```html
{:eval; {:snippet; snippet-name :} >>
    <li>{:;__eval__:}</li>
:}
```

```html
{:eval; {:snippet; snippet-name :} >>
    <li>{:snippet; snippet-name :}</li>
:}
```

This is also possible

```html
{:eval; {:;varname1:}{:;varname2:} >>
    ...
    {:;__eval__:}
    ...
:}
```

```html
{:eval;
    {:code;
        ... a lot of code here ...
    :}
    >>
    ...
    {:;__eval__:}
    ...
:}
```

Can also be used to prevent output, in the following example, we want the include to show a possible output:

```html
{:+eval; {:include; file :} >> :}
```

For more details about the "+" modifier see "modifiers".

---