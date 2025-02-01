{:; ... :} (var)
================

Output var value.

```html
{:;varname:}
{:;array->key:}
```

Modifiers:
----------

```html
{:^;varname:}
```

Assuming that the value of "varname" is "value":

```html
<div></div>

{:;varname:}

<div></div>

{:^;varname:}
```

Output:

```html
<div></div>

value

<div></div>value
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

```html
{:;arr->0:}
{:;obj->0:}
{:;obj->arr->0:}
```

Dynamic evaluation
------------------

```html
{:;array->{:;key:}:}
```

However, the following will produce an error:

```html
{:;{:;varname:}:}
```

For safety reasons, when evaluating the complete variable it is necessary to use "allow":

```html
{:; {:allow; allowed-words-list >> {:;varname:} :} :}
```

In any case, you must use "allow" on any variable that comes from the context. See the "allow" and "declare" bifs for more details.

Undefined
---------

It is not an error to use an undefined variable or an array, nor will it show any warning, in the case of an array it will show an empty string:

```html
<div>{:;undefvar:}</div>
<div>{:;array:}</div>
```

Output:

```html
<div></div>
<div></div>
```

---