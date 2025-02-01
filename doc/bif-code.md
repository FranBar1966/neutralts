{:code; ... :}
==============

Output code without action.

In some cases we need a block of code, "code" does nothing, simply encloses in block. It also serves as a wrapper to create parameters.

```html
{:code; code :}

{:code; This is always shown :}
```

Modifiers:
----------

```html
{:+code; ... :}
{:^code; ... :}
```

For more details about the "+" modifier see "modifiers".

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

Flags
-----

```html
{:code; {:flg; safe noparse encode_tags encode_bifs encode_tags_after :} >> ... :}
```

### Flag: noparse

Prevent the block's bifs from being parsed, assuming that the value of varname is value:

```html
{:code;
    <div>{:;varname:}</div>
:}
{:code; {:flg; noparse :} >>
    <div>{:;varname:}</div>
:}
```

Output:

```html
<div>value</div>
<div>{:;varname:}</div>
```

### Flag: encode_tags

Encoding html tags, assuming that the value of varname is value:

```html
{:code;
    <div>{:;varname:}</div>
:}
{:code; {:flg; encode_tags :} >>
    <div>{:;varname:}</div>
:}
```

Output:

```html
<div>value</div>
&lt;div&gt;value&lt;&#x2F;div&gt;
```

### Flag: encode_bifs

Encoding bifs, when "{:" and ":}" characters are encoded, the bifs will not be parsed, assuming that the value of varname is value:

```html
{:code;
    <div>{:;varname:}</div>
:}
{:code; {:flg; encode_bifs :} >>
    <div>{:;varname:}</div>
:}
```

Output:

```html
<div>value</div>
<div>&#123;:;varname:&#125;</div>
```

### Flag: safe

Encoding all, safe implies noparse, encode_tags and encode_bifs, assuming that the value of varname is value:

```html
{:code;
    <div>{:;varname:}</div>
:}
{:code; {:flg; safe :} >>
    <div>{:;varname:}</div>
:}
```

Output:

```html
<div>value</div>
&lt;div&gt;&#123;:;varname:&#125;&lt;&#x2F;div&gt;
```

### Flag: encode_tags_after

Encoding html tags after parsing, assuming that the content of "file.ntlp" is:

```html
<div></div>
```

Then:

```html
{:code; {:flg; encode_tags_after :} >>
    {:include; file.ntlp :}
:}
```

Output:

```html
&lt;div&gt;&lt;&#x2F;div&gt;
```

Nesting
-------

Can be nested (no limit):

```html
{:code;
    {:code;
        {:code;
            ...
        :}
    :}
:}
```

Grouping:

```html
{:coalesce;
    {:code; {:* block 1 *:}
        {:code; ... :}
        {:code; ... :}
        {:code; ... :}
    :}
    {:code; {:* block 2 *:}
        {:code; ... :}
    :}
:}
```

Params
------

If we need to create parameters they must necessarily reside in a "code" block:

```html
{:code;
    {:param; ... :}
    {:param; ... :}
    ...
:}
```

See the bif "param" for more information on parameters.

---
