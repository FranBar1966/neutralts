Neutral Web Template Engine
===========================

Neutral is a **web application template system**, designed to work with **any programming language** (language-agnostic) via IPC and natively as library/crate in Rust.

In the examples, we use exactly the same template for both Rust and PHP:

- [Rust example](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/actix)
- [PHP example](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/php)
- [Template](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/www)


Safe
----

Neutral is developed in Rust, one of the most secure programming languages. It does not have access to the application's data; it cannot do so because it is designed this way. It implements security mechanisms like "allow," which prevent arbitrary files from being loaded into templates.

Features
--------

It allows you to create templates compatible with any system and any programming language.

* Safe
* Language-agnostic
* Modular
* Parameterizable
* Efficient
* Parse files
* Embed files
* Localization
* Loops: for and each
* Snippets
* Nesting, grouping and wrapping
* Redirections: HTTP y JavaScript
* Exit with error: 403, 404, 503, ...
* Comments

How it works
------------

Neutral TS offers two main ways to integrate with other programming languages:

* In Rust: You can use Neutral TS as a library by downloading the crate.

* In other programming languages: Inter-Process Communication (IPC) is necessary, similar to how databases like MariaDB work.

Imagine a database. It has a server, and different programming languages access the data through a client. This means that if you run a "SELECT ..." query from any programming language, the result will always be the same.

Similarly, Neutral TS has an IPC server, and each programming language has a client. No matter where you run the template, the result will always be the same.

Thanks to this, and to its modular and parameterizable design, it is possible to create utilities or plugins that will work everywhere. For example, you can develop tools to create forms or form fields and create your own libraries of "snippets" for repetitive tasks.

A small example of a plugin: [countries form field](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/countries-form-field) and another one more practical: [plugin build-form](https://gitlab.com/neutralfw/neutralts/-/tree/master/plugins/build-form)

Localization
------------

Neutral provides powerful and easy-to-use translation utilities... define the translation in a JSON:

```json
"locale": {
    "current": "en",
    "trans": {
        "en": {
            "Hello": "Hello",
            "ref:greeting-nts": "Hello"
        },
        "es": {
            "Hello": "Hola",
            "ref:greeting-nts": "Hola"
        },
        "de": {
            "Hello": "Hallo",
            "ref:greeting-nts": "Hallo"
        },
        "fr": {
            "Hello": "Bonjour",
            "ref:greeting-nts": "Bonjour"
        },
        "el": {
            "Hello": "Γεια σας",
            "ref:greeting-nts": "Γεια σας"
        }
    }
}
```

Now you can use:

```neutral
{:trans; Hello :}
```

Actually you can always use "trans" because if there is no translation it returns the text.

Bif layout (Build-in function)
------------------------------

```neutral

    .-- open bif
    |    .-- bif name
    |    |   .-- name separator
    |    |   |    .-- params
    |    |   |    |    .-- params/code separatos
    |    |   |    |    |    .-- code
    |    |   |    |    |    |   .-- close bif
    |    |   |    |    |    |   |
    v    v   v    v    v    v   v
    -- ----- - ------- -- ----- --
    {:snippet; varname >>  ...  :}
    ------------------------------
            ^  ----------------
            |         ^
            |         |
            |         `-- source
            `-- Build-in function

```

Bif example:

```neutral
{:filled; varname >>
    Hello!
:}
```

Neutral is based on Bifs with block structure, we call the set of nested Bifs of the same level a block:

```neutral

              .-- {:coalesce;
              |       {:code;
              |           {:code; ... :}
              |           {:code; ... :}
    Block --> |           {:code; ... :}
              |       :}
              |       {:code;
              |           {:code; ... :}
              |       :}
              `-- :}

                  {:coalesce;
              .------ {:code;
              |           {:code; ... :}
    Block --> |           {:code; ... :}
              |           {:code; ... :}
              `------ :}
              .------ {:code;
    Block --> |           {:code; ... :}
              `------ :}
                  :}

```

Short circuit at block level, if varname is not defined, the following ">>" is not evaluated:

```neutral
{:defined; varname >>
    {:code;
        {:code;
            ...
        :}
    :}
:}
```

By design all Bifs can be nested and there can be a Bif anywhere in another Bif except in the name.

Data
----

The data is defined in a JSON:

```json
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
```

And they are displayed with the bif {:; ... :} (var)

Simple variable:

```neutral
{:;hello:}
```

Arrays with the "->" operator

```neutral
{:;array->hello:}
```

Snippets
--------

Snippet is a tool that can be used in a similar way to a function, it defines a snippet:

```neutral
{:snippet; name >>
    Any content here, including other snippet.
:}
```

From then on you can invoke it like this:

```neutral
{:snippet; name :}
```

Template example
----------------

```html
{:*
    comment
*:}
{:locale; locale.json :}
{:include; theme-snippets.ntpl :}
<!DOCTYPE html>
<html lang="{:lang;:}">
    <head>
        <title>{:trans; Site title :}</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        {:snippet; current-theme:head :}
        <link rel="stylesheet" href="bootstrap.min.css">
    </head>
    <body class="{:;body-class:}">
        {:snippet; current-theme:body_begin  :}
        {:snippet; current-theme:body-content :}
        {:snippet; current-theme:body-footer  :}
        <script src="jquery.min.js"></script>
    </body>
</html>
```

Native use (Rust)
-----------------

You need two things, a template file and a json schema:

```plaintext

let schema = json!({
    "config": {
        "comments": "remove"
    },
    "inherit": {
        "locale": {
            "current": "en",
            "trans": {
                "en": {
                    "Hello nts": "Hello",
                    "ref:greeting-nts": "Hello"
                },
                "es": {
                    "Hello nts": "Hola",
                    "ref:greeting-nts": "Hola"
                },
                "de": {
                    "Hello nts": "Hallo",
                    "ref:greeting-nts": "Hallo"
                },
                "fr": {
                    "Hello nts": "Bonjour",
                    "ref:greeting-nts": "Bonjour"
                },
                "el": {
                    "Hello nts": "Γεια σας",
                    "ref:greeting-nts": "Γεια σας"
                }
            }
        }
    },
    "data": {
        "web-site-name": "MySite",
        "varname": "value",
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
});
```

Template file.ntpl:

```text
{:;web-site-name:}
```

In Rust:

```text
let template = Template::from_file_value("file.ntpl", schema).unwrap();
let content = template.render();

// e.g.: 200
let status_code = template.get_status_code();

// e.g.: OK
let status_text = template.get_status_text();

// empty if no error
let status_param = template.get_status_param();

// act accordingly at this point according to your framework
```

Rust examples
-------------

 - [actix-web](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/actix)
 - [warp](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/warp)
 - [axum](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/actix)
 - [rocket](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/rocket)
 - [examples](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples)

PHP
---
- [example](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/php)
- [IPC client](https://gitlab.com/neutralfw/neutralts/-/tree/master/ipc/php)

Python
------
- [example](https://gitlab.com/neutralfw/neutralts/-/tree/master/examples/python)
- [IPC client](https://gitlab.com/neutralfw/neutralts/-/tree/master/ipc/python)

------

[Download](https://crates.io/api/v1/crates/neutralts/1.0.0/download)

