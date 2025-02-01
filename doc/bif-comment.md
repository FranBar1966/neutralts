{:* comment *:}
===============

```html
{:* This is a comment *:}

{:*
    This is a comment
    -----------------
*:}

{:*
    Nested comment
    --------------
    {:* comment
        {:* comment
            {:* ... *:}
        *:}
    *:}
*:}
```

Comment inside build-in function:

```html
{:; varname {:* comment *:} :}

{:code; {:* comment *:}
    {:param; parvalue {:* comment *:} :}
    {:param; parvalue :} {:* comment *:}
    ...
:}
```

The only place where we cannot insert a comment is the bif name, any other location is acceptable.

---
