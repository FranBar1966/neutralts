{:exit; ... :}
==============

Terminate the current template with status code, 200 by default. No output.

```html
{:exit; HTTP-STATUS-CODE :}

{:exit; :}
```

It is important to know that the **status codes must be managed by the application**, this bif is limited to set them and to terminate the template.

In addition, in **status codes 400 to 599, 301, 302, 303, 307 and 308** the rendered **content is removed** and replaced by the status code.

Modifiers:
----------

```html
{:!exit; ... :}
```

### Modifier: ! (not)

The "not" modifier prevents termination, continues executing the template and is limited only to setting a status code:

```html
{:!exit; 202 :}
```

No flags
--------

Some uses
---------

In the following examples, the template is terminated and a status code is set:

```html
{:exit; 401 :}
{:exit; 403 :}
{:exit; 404 :}
{:exit; 503 :}
```

A parameter is set here:

```html
{:exit; 500 >> reason :}
```

Redirect
--------

With status codes 301, 302, 303, 307 and 308 you can create a redirect by adding the URL to the parameters:

```html
{:exit; 301 >> /page :}
{:exit; 302 >> /page :}
{:exit; 303 >> /page :}
{:exit; 307 >> https://example.com :}
{:exit; 308 >> https://example.com :}
```

The "redirect" bif also performs this task.

Custom status codes
-------------------

Status codes from 100 to 999 are used or could be used in the future by the HTTP protocol, so it is better not to use them, but we could use a larger code to create our custom status codes.

For example, if we want to change the behavior of the 404 error where the content is removed when it is set, the status code “10404” could be used

```html
{:exit; 10404 :}
```

Or:

```html
{:exit; 10401 >> reason :}
```

And manage it in the application in another way.

Manage in the app (native Rust)
-------------------------------

If you use the bif “exit” or “redirect” it is necessary to manage the status codes in the application, it will depend on the environment or framework you are using, it could be something like this:

```text
let template = Template::from_file_value("file.ntpl", schema).unwrap();
let content = template.render();

// e.g.: 500
let status_code = template.get_status_code();

// e.g.: Internal Server Error
let status_text = template.get_status_text();

// e.g.: template error x
let status_param = template.get_status_param();

// act accordingly at this point
```

It may be the case that the template contains a syntax error, in which case set the status code 500 and in the parameter the reason, by default the content is blank.

Manage in the app (others)
--------------------------

Each programming language can implement it in a different way, see the IPC client of each language.

There will usually be an equivalent function with the same name as those in Rust.

---
