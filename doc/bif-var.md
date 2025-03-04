{:; ... :} (var)
================

Output var value.

```text
{:;varname:}
{:;array->key:}
```

Modifiers:
----------

```text
{:^;varname:}
{:&;varname:}
{:!;varname:}
```

### Modifier: ^ (upline)

Assuming that the value of "varname" is "value":

```text
<div></div>

{:;varname:}

<div></div>

{:^;varname:}
```

Output:

```text
<div></div>

value

<div></div>value
```

### Modifier: & (filter)

Escapes special HTML characters and braces:

```text
& → &amp;
< → &lt;
> → &gt;
" → &quot;
' → &#x27;
/ → &#x2F;
{ → &#123;
} → &#125;
```

By default all user variables are filtered, those starting with `CONTEXT->`. There is also a schema configuration to escape all variables `filter_all`:

```text
{
    "config": {
        "filter_all": true
    },
    "inherit": {},
    "data": {}
}
```

Default is false.

### Modifier: ! (not)

Does not filter special HTML characters and braces, if combined with `&` the result is no filtering.

Avoid filtering a variable:

```text
{:!;CONTEXT->GET->var:}
```

The contradictory combination with `&` results in no filtering:

```text
{:&!;varname:}
```

No flags
--------

Arrays
------

To access an array, use: "->", no distinction between objects and arrays.
Assuming:

```json
{
    "data": {
        "arr": [
            "value"
        ],
        "obj": {
            "0": "value"
            "arr": [
                "value"
            ],
        }
    }
}
```

Then:

```text
{:;arr->0:}
{:;obj->0:}
{:;obj->arr->0:}
```

Dynamic evaluation
------------------

```text
{:;array->{:;key:}:}
```

However, the following will produce an error:

```text
{:;{:;varname:}:}
```

For safety reasons, when evaluating the complete variable it is necessary to use "allow":

```text
{:; {:allow; allowed-words-list >> {:;varname:} :} :}
```

In any case, you must use "allow" on any variable that comes from the context. See the "allow" and "declare" bifs for more details.

Undefined
---------

It is not an error to use an undefined variable or an array, nor will it show any warning, in the case of an array it will show an empty string:

```text
<div>{:;undefvar:}</div>
<div>{:;array:}</div>
```

Output:

```text
<div></div>
<div></div>
```

---
