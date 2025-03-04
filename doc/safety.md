Safety
======

By design the templates do not have access to arbitrary application data, the data has to be passed to the template in a JSON, then the data that you have not included in the JSON cannot be read by the template.

Variables
---------

By design the value of the variables is not evaluated:

```text
{
    "data": {
        "inject": "{:exit;:}",
    }
}
```

Then:

```text
<div>{:;inject:}</div>
<div>{:eval; {:;inject:} >> {:;__eval__:} :}</div>
<div>{:code; {:;inject:} :}</div>
<div>{:code; {:code; {:;inject:} :} :}</div>
```

In no case is `{:exit;:}` evaluated, output:

```text
<div>{:exit;:}</div>
<div>{:exit;:}</div>
<div>{:exit;:}</div>
<div>{:exit;:}</div>
```

This is especially important when someone tries to do this:

```text
{
    "data": {
        "inject": "{:include; /path/to/secrets :}"
    }
}
```

When `cache_disable = false` on all values, possible bifs are filtered:

```text
<div>{:;inject:}</div>
<div>{:eval; {:;inject:} >> {:;__eval__:} :}</div>
<div>{:code; {:;inject:} :}</div>
<div>{:code; {:code; {:;inject:} :} :}</div>
```

Output:

```text
<div>&#123;:exit;:&#125;</div>
<div>&#123;:exit;:&#125;</div>
<div>&#123;:exit;:&#125;</div>
<div>&#123;:exit;:&#125;</div>
```

Note the following example:

```text
{
    "data": {
        "secret": "123456",
        "reference": "secret"
    }
}
```

The following will produce the error `insecure varname`:

```text
{:; {:;reference:} :}
```

To evaluate a complete variable you must use `allow` or evaluate partially:

```text
{:; anything-{:;reference:} :}
```

The reason it can be partially evaluated is to be able to do this:

```text
{:; array->{:;key:} :}
```

In the same way that you can do something similar in any programming language:

```text
$array[$key]
```

In this case you should take precautions or use `allow`, and as a rule, **NEVER evaluate variables that come from the user**, GET, POST, COOKIES, ENV, ... if you are not using `allow`:

```text
{:declare; valid >>
    word1
    word2
:}

{:;
    {:allow; valid >> {:;reference:} :}
:}
```

### {:code; ... :}

Unsafe variables can be displayed in a `code` block:

```text
{
    "data": {
        "inject": "<div>{:exit;:}</div>",
    }
}
```

Then:

```text
{:;inject:}
{:code; {:flg; safe :} >> {:;inject:} :}
{:code; {:flg; encode_tags_after :} >> {:;inject:} :}
```

Output:

```text
<div>{:exit;:}</div>
&#123;:;inject:&#125;
&lt;div&gt;{:exit;:}&lt;&#x2F;div&gt;
```

Files
-----

The following will produce the error `insecure file name`:

```text
{:include; {:;varname:} :}
```

To evaluate a complete variable you must use `allow` or evaluate partially:

```text
{:include; anything-{:;varname:} :}
```

It is best to always use `allow` in `include` when using a variable in the file name, including the case of partial evaluation, and as a rule, **NEVER evaluate variables that come from the user**, GET, POST, COOKIES, ENV, ... if you are not using `allow`:

```text
{:declare; valid-files >>
    home.ntpl
    login.ntpl
    error.ntpl
:}

{:include;
    {:allow;
        valid-files >> {:;varname:}
    :}{:else;
        error.ntpl
    :}
:}
```

Cross-Site Scripting (XSS)
--------------------------

There is a space reserved in the schema for variables coming from the user:

```text
{
    "config": {},
    "inherit": {},
    "data": {
        "CONTEXT": {
            "ROUTE": "",
            "HOST": "",
            "GET": {},
            "POST": {},
            "HEADERS": {},
            "REQUEST": {},
            "FILES": {},
            "COOKIES": {},
            "SESSION": {},
            "ENV": {}
        }
    }
}
```

All `CONTEXT` variables are filtered automatically:

```text
& → &amp;
< → &lt;
> → &gt;
" → &quot;
' → &#x27;
/ → &#x2F;
{ → &#123;
} → &#125;
```

However, you must take care of assigning the variables coming from the user to `CONTEXT` in your application. This way of proceeding allows the templates to know the insecure variables, moreover, they can be identified at a glance in the code.

The variable **names is as unsafe** as its value and is filtered by default.

There is also a schema configuration to escape all variables `filter_all`:

```text
{
    "config": {
        "filter_all": true
    },
    "inherit": {},
    "data": {}
}
```

Default is false.

Rules
-----

* Never trust on the context: GET, POST, COOKIES, ENV, ...
* In the application never trust that the templates take care of security.
* In the templates never trust that the application is in charge of security.

Act in your application as if the templates were insecure and filter all variables coming from the user and from insecure sources, do the same in your template, filter all variables from insecure sources.

---
