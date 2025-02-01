{:bool; ... :}
===========================

Output code if a variable is true

```html
{:bool; variable >> code :}

{:bool; varname >> this shown if varname is true :}
```

Modifiers:
----------

```html
{:!bool; varname >> ... :}
{:^bool; varname >> ... :}
```

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

### Modifier: ! (not):

```html
{:!bool; varname >> this shown if varname is false :}
```

No flags
--------

Examples
--------

```html
{:bool; true          >> Shown! :}
{:bool; false         >> Not shown :}
{:bool; hello         >> Shown! :}
{:bool; zero          >> Not shown :}
{:bool; one           >> Shown! :}
{:bool; spaces        >> Shown! :}
{:bool; empty         >> Not shown :}
{:bool; null          >> Not shown :}
{:bool; undef         >> Not shown :}
{:bool; undefarr      >> Not shown :}
{:bool; emptyarr      >> Not shown :}
{:bool; array         >> Shown! :}
{:bool; array->true   >> Shown! :}
{:bool; array->false  >> Not shown :}
{:bool; array->hello  >> Shown! :}
{:bool; array->zero   >> Not shown :}
{:bool; array->one    >> Shown! :}
{:bool; array->spaces >> Shown! :}
{:bool; array->empty  >> Not shown :}
{:bool; array->null   >> Not shown :}
{:bool; array->undef  >> Not shown :}
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
