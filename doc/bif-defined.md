{:defined; ... :}
=================

Output code if a variable is defined

```html
{:defined; variable >> code :}

{:defined; varname >> this shown if varname is defined :}
```
Modifiers:
----------

```html
{:^defined; ... :}
{:!defined; ... :}
{:+defined; ... :}
```

For more details about the "+" modifier see "modifiers".

### Modifier: ! (not)

```html
{:!defined; varname >> this shown if varname is not defined :}
```

No flags
--------

Examples
--------

```html
{:defined; true          >> Shown! :}
{:defined; false         >> Shown! :}
{:defined; hello         >> Shown! :}
{:defined; zero          >> Shown! :}
{:defined; one           >> Shown! :}
{:defined; spaces        >> Shown! :}
{:defined; empty         >> Shown! :}
{:defined; null          >> Not shown :}
{:defined; undef         >> Not shown :}
{:defined; undefarr      >> Not shown :}
{:defined; emptyarr      >> Shown! :}
{:defined; array         >> Shown! :}
{:defined; array->true   >> Shown! :}
{:defined; array->false  >> Shown! :}
{:defined; array->hello  >> Shown! :}
{:defined; array->zero   >> Shown! :}
{:defined; array->one    >> Shown! :}
{:defined; array->spaces >> Shown! :}
{:defined; array->empty  >> Shown! :}
{:defined; array->null   >> Not shown :}
{:defined; array->undef  >> Not shown :}
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
