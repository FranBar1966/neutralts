{:array; ... :}
============================

Output code if a variable is array.

```html
{:array; variable >> code :}

{:array; varname >> this shown if varname is array :}
```

Note that there is no distinction between objects and arrays.

Modifiers:
----------

```html
{:!array; ... :}
{:+array; ... :}
{:^array; ... :}
```

For more details about the "+" modifier see "modifiers".

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

### Modifier: not

```html
{:!array; varname >> this shown if varname is not array :}
```

No flags
--------

Examples
--------

```html
{:array; true          >> Not shown :}
{:array; false         >> Not shown :}
{:array; hello         >> Not shown :}
{:array; zero          >> Not shown :}
{:array; one           >> Not shown :}
{:array; spaces        >> Not shown :}
{:array; empty         >> Not shown :}
{:array; null          >> Not shown :}
{:array; undef         >> Not shown :}
{:array; undefarr      >> Not shown :}
{:array; emptyarr      >> Shown! :}
{:array; array         >> Shown! :}
{:array; array->true   >> Not shown :}
{:array; array->false  >> Not shown :}
{:array; array->hello  >> Not shown :}
{:array; array->zero   >> Not shown :}
{:array; array->one    >> Not shown :}
{:array; array->spaces >> Not shown :}
{:array; array->empty  >> Not shown :}
{:array; array->null   >> Not shown :}
{:array; array->undef  >> Not shown :}
```

Assumes data:

```json
{
    "data": {
        "true": true,
        "false": false,
        "hello": "hello",
        "zero": "0",
        "one": "1",
        "spaces": "  ",
        "empty": "",
        "null": null,
        "emptyarr": [],
        "array": {
            "true": true,
            "false": false,
            "hello": "hello",
            "zero": "0",
            "one": "1",
            "spaces": "  ",
            "empty": "",
            "null": null
        }
    }
}
```

---
