{:declare; ... :}
=================

Defines a list of allowed words separated by spaces for the bif "allow", no output.

```html
{:declare; name >> words list :}
```
Note that declare **must be defined in a file whose name contains the word "snippet".** An error will occur if an attempt is made to define it elsewhere.

Modifiers:
----------

```html
{:^declare; ... :}
```

No flags
--------

Wildcards
---------

* (.) Dot, that matches any character.
* (?) Question, that matches exactly one character.
* (*) Asterisk, that matches zero or more characters.

Use app data
------------

Assumes:

```json
{
    "data": {
        "themes": [
            "sketchy",
            "flatly",
            "darkly",
            "slate",
            "united"
        ]
    }
}
```

Then:

```html
{:declare; themes >>
    {:each; themes key theme >>
        {:;:} {:;theme:}
    :}
:}
```

Unprintable {:;:} is necessary to preserve a space between words.

Examples
--------

```html
{:declare; example >>
    en-??
    en_??
    en.US
    en?UK
:}
```

```html
{:declare; languages >>
    en
    en-??
    en_??
    es
    es-??
    es_??
:}
```

```html
{:declare; templates >>
    *.ntpl
:}
```

```html
{:declare; colors >> red green blue :}
```

```html
{:declare; any >> * :}
```

---