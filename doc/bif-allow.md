{:allow; ... :}
===================================

Output literal if the literal found from a list defined with "declare", empty string if it fails.

```html
{:allow; declare-name >> literal :}

{:allow; allowed-words-list >> {:;varname:} :}
```
In the above the output will be the content of varname, if that content is supported by allowed-words-list.

It is mainly used for safety and its most common use is this one:

```html
{:include; {:allow; allowed-words-list >> {:;varname:} :} :}
{:include; {:!allow; traversal >> {:;varname:} :} :}
```

In the first case it only supports values that reside in the word list, preventing arbitrary files from being accessed. The second case does not allow directory traversal.

It is convenient to set a default value, as failure to do so will output an empty string:

```html
{:include;
    {:allow;
        allowed-words-list >> {:;varname:}
    :}{:else:
        secure or default value
    :}
:}
```

Or:

```html
{:include;
    {:allow;
        allowed-words-list >> {:;varname:}
    :}{:else:
        {:exit; 403 :}
    :}
:}
```

Modifiers:
----------

```html
{:!allow; ... :}
{:^allow; ... :}
```

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

### Modifier: ! (not)

Output of an empty string in case it is found in the "declare".

Flags
-----

```html
{:allow; {:flg; partial casein replace :} name >> ... :}
```

### Flag: partial

It would be the equivalent of having wildcards in the word list, from “word” to “*word*”.

### Flag: casein

Case insensitive

### Flag: replace

Returns the word found (without wildcards) instead of the evaluation text.

Word declaration
----------------

With "declare" we define the list of words to be allowed or denied:

```html
{:declare; files >>
    home.tpl
    contact.tpl
    about.tpl
:}

{:declare; traversal >>
    /*
    \\\\*
    *\\.\\.*
:}
```

Then, the following will produce an error:

```html
{:include;
    {:allow;
        files >> passwd
    :}{:else;
        {:exit; 403 :}
    :}
:}
```

An error will also occur here:

```html
{:include;
    {:!allow;
        traversal >> ../dir/file
    :}{:else;
        {:exit; 403 :}
    :}
:}
```

The most successful method to do this is the first one, where only the declared files are supported.

Declare supports wildcards, see bif "declare" for details.

Examples
--------

Assumes:

```html
{:*
    Allow any template file
*:}
{:declare; templates >>
    *.ntpl
:}
```

Then:

```html
<div>{:allow; templates >> file.txt :}{:else; fails :}</div>
<div>{:allow; templates >> file.ntpl :}{:else; fails :}</div>
```

Output:

```html
<div>fails</div>
<div>file.ntpl</div>
```

Assumes:

```html
{:*
    Allow languages
*:}
{:declare; languages >>
    en
    en-??
    en_??
    es
    es-??
    es_??
:}
```

Then:

```html
<div>{:allow; languages >> fr :}{:else; fails :}</div>
<div>{:allow; languages >> es-ES :}{:else; fails :}</div>
```

Output:

```html
<div>fails</div>
<div>es-ES</div>
```

Assumes:

```html
    {:*
        Allow languages
    *:}
    {:declare; languages >>
        en
        en???
        es
        es???
    :}
```

Then:

```html
    <div>{:allow; {:flg; replace :} languages >> de :}{:else; en :}</div>
    <div>{:allow; {:flg; replace :} languages >> es-ES :}{:else; en :}</div>
```

Output:

```html
    <div>en</div>
    <div>es</div>
```

---
