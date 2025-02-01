{:locale; ... :}
================

Includes a language json file:

```html
{:locale; filename :}

{:locale; file.json :}
```

The language files must have a structure similar to this one:

```json
{
    "trans": {
        "es": {
            "Hello": "Hola",
            "ref:greeting": "Hola",
        },
        "es-ES": {
            "Hello": "Hola",
            "ref:greeting": "Hola",
        }
    }
}
```

A "trans" key and then the key for each language, any other key will produce an error or be ignored.

Modifiers:
----------

```html
{:!locale; ... :}
{:^locale; ... :}
```

### Modifier: ! (not)

The "not" modifier prevents the file from being reload if it has already been parsed. Generally, language files should only be included once, it will increase performance if "not" is used:

```html
{:!locale; file.json :}
```

Flags
-----

```html
{:locale; {:flg; require noparse :} >> ... :}
```

### Flag: require

By default, no error will occur if the file to locale does not exist, unless the "require" flag is set.

```html
{:locale; {:flg; require :} >> file.json :}
```

### Flag: noparse

The "noparse" flag prevents the file to be included from being parsed.

```html
{:locale; {:flg; noparse :} >> file.json :}
```

Return value
------------

"locale" show no output but returns "{:;:}" (unprintable) if successful, so this is possible:

```html
{:locale; file.{:lang;:}.json :}
{:else; file.en.json :}
```

Dynamic evaluation
------------------

The following will produce an error:

```html
{:locale; {:;varname:} :}
```

For safety reasons, when evaluating the complete variable it is necessary to use "allow":

```html
{:locale; {:allow; allowed-words-list >> {:;varname:} :} :}
{:locale; {:!allow; traversal >> {:;varname:} :} :}
```

In any case, you must use "allow" on any variable that comes from the context. See the "allow" and "declare" bifs for more details.

Translation evaluation
----------------------

Translations may contain variables:

```json
{
    "trans": {
        "es": {
            "Welcome to {:;web-site-name:}": "Bienvenido a {:;web-site-name:}"
        }
    }
}
```

Variables are resolved at the time the file is included.

(*) Translations included in the "schema" are not evaluated, only those loaded with "locale".

Relative to current file path
-----------------------------

We can use relative paths to the currently localed file with the "#" symbol:

```html
{:locale; #/file.json :}
```

It will be relative to the file loaded with "include":

```html
{:*
    file: /path/to/tpl/snippets.ntpl
    Here #/file.json is: /path/to/tpl/file.json
*:}

{:locale; #/file.json :}
```

---