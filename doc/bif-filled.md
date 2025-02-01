{:filled; ... :}
================

Output code  if a variable is filled (non-zero length).

```html
{:filled; variable >> code :}

{:filled; varname >> this shown if varname is filled :}
```

Modifiers:
----------

```html
{:^filled; varname >> ... :}
{:!filled; varname >> ... :}
{:+filled; varname >> ... :}
```

For more details about the "+" modifier see "modifiers".

### Modifier ! (not):

```html
{:!filled; varname >> this shown if varname is not filled :}
```

No flags
--------

Examples
--------

```html
{:filled; true          >> Shown! :}
{:filled; false         >> Shown! :}
{:filled; hello         >> Shown! :}
{:filled; zero          >> Shown! :}
{:filled; one           >> Shown! :}
{:filled; spaces        >> Shown! :}
{:filled; empty         >> Not shown :}
{:filled; null          >> Not shown :}
{:filled; undef         >> Not shown :}
{:filled; undefarr      >> Not shown :}
{:filled; emptyarr      >> Not shown :}
{:filled; array         >> Shown! :}
{:filled; array->true   >> Shown! :}
{:filled; array->false  >> Shown! :}
{:filled; array->hello  >> Shown! :}
{:filled; array->zero   >> Shown! :}
{:filled; array->one    >> Shown! :}
{:filled; array->spaces >> Shown! :}
{:filled; array->empty  >> Not shown :}
{:filled; array->null   >> Not shown :}
{:filled; array->undef  >> Not shown :}
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