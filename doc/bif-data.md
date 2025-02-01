{:data; ... :}
==============

Set local data from json file.

```html
{:data; local-data.json :}
```
The scope of the data is the file where it is loaded and its children.

To access the variables, the prefix "local::" must be used:

```html
{:;local::varname:}
```
Modifiers
---------

```html
{:!data; ... :}
{:^data; ... :}
```
The "not" modifier prevents the file from being reload if it has already been parsed.

```html
{:!data; file.json :}
```

Flags
-----

```html
{:data; {:flg; inline :} >> ... :}
```

### Flag: inline

```html
{:data; {:flg; inline :} >>
    {
        "data": {
            "varname": "value"
        }
    }
:}
```
Examples
--------

Assumes local-data.json:

```json
{
    "data": {
        "hello": "Hello!"
    }
}
```

Then:

```html
{:data; local-data.json :}
{:;local::hello:}
```

Output:

```html
Hello!
```

---