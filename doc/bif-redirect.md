{:redirect; ... :}
==================

Terminate the current template with redirect status code or Javascript redirect.

```html
{:redirect; 301 >> url :}
{:redirect; js:reload:top :}
```

It is important to know that the **status codes must be managed by the application**, this bif is limited to set them and to terminate the template. In the case of JS redirections, a status code “200 OK” is set and does not need to be managed in the app.

Modifiers:
----------

```html
{:^redirect; ... :}
```

No flags
------

Redirect HTTP
-------------

The possible values for HTTP redirects are 301, 302, 303, 307 and 308 any other will generate an error. Redirect codes:

```html
{
    "301": "Moved Permanently",
    "302": "Found",
    "303": "See Other",
    "307": "Temporary Redirect",
    "308": "Permanent Redirect"
}

{:redirect; 301 >> http://example.com :}
{:redirect; 302 >> http://example.com :}
{:redirect; 303 >> http://example.com :}
{:redirect; 307 >> http://example.com :}
{:redirect; 308 >> http://example.com :}
```

Custom redirections can also be created with the “exit” bif.

Redirect Javascript
-------------------

In this case it is not necessary to do anything in the app.

js:reload:top reloads the current page in the top window, no URL required:

```html
{:redirect; js:reload:top :}
```

js:reload:self reloads the current page in the current window, no URL required:

```html
{:redirect; js:reload:self :}
```

js:redirect:top redirects the page (URL) in the top window, requires the destination URL:

```html
{:redirect; js:redirect;top >> /home/ :}
```

js:redirect:self redirects the page (URL) in the current window, requires the destination URL:

```html
{:redirect; js:redirect;self >> /home/ :}
```

Manage in the app (native Rust)
-------------------------------

If you use the bif “exit” or “redirect” it is necessary to manage the status codes in the application, it will depend on the environment or framework you are using, it could be something like this:

```text
let template = Template::from_file_value("file.ntpl", schema).unwrap();
let content = template.render();

// e.g.: 301
let status_code = template.get_status_code();

// e.g.: Moved Permanently
let status_text = template.get_status_text();

// e.g.: https://example.com
let status_param = template.get_status_param();

// act accordingly at this point
```

It may be the case that the template contains a syntax error, in which case set the status code 500 and in the parameter the reason, by default the content is blank.

Manage in the app (others)
--------------------------

Each programming language can implement it in a different way, see the IPC client of each language.

There will usually be an equivalent function with the same name as those in Rust.

---
