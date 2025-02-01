{:include; ... :}
=================

Include and usually parse any file, usually a template.

```html
{:include; filename :}

{:include; template.ntpl :}
```

Modifiers:
----------

```html
{:!include; ... :}
{:^include; ... :}
```

### Modifier: ! (not)

The "not" modifier prevents the file from being reparse if it has already been parsed.

Assuming that the content of file.ntpl is simply the word "Hello":

```html
{:include; file.ntpl :}
...
{:include; file.ntpl :}
```

Output:

```html
Hello
Hello
```

With "not":

```html
{:include; file.ntpl :}
...
{:!include; file.ntpl :}
```

Output:

```html
Hello
```

The following produces the same result as above:

```html
{:!include; file.ntpl :}
...
{:!include; file.ntpl :}
```

Or can the parse be forced:

```html
{:!include; file.ntpl :}
...
{:include; file.ntpl :}
```

Output:

```html
Hello
Hello
```

Flags
-----

```html
{:include; {:flg; require noparse safe :} >> ... :}
```

### Flag: require

By default, no error will occur if the file to include does not exist, unless the "require" flag is set.

```html
{:include; {:flg; require :} >> file.ntpl :}
```

### Flag: noparse

The "noparse" flag prevents the file to be included from being parsed.

```html
{:include; {:flg; noparse :} >> file.css :}
```

### Flag: safe

Encoding all, safe implies noparse.

```html
{:include; {:flg; safe :} >> file.txt :}
```

Dynamic evaluation
------------------

The following will produce an error:

```html
{:include; {:;varname:} :}
```

For safety reasons, when evaluating the complete variable it is necessary to use "allow":

```html
{:include; {:allow; allowed-words-list >> {:;varname:} :} :}
{:include; {:!allow; traversal >> {:;varname:} :} :}
```

In any case, you must use "allow" on any variable that comes from the context. See the "allow" and "declare" bifs for more details.

Relative to current file path
-----------------------------

When creating a web application, we'll know where the files are located, so we can do:

```html
{:include; /path/to/tpl/template.ntpl :}
```

We can use relative paths to the currently included file with the "#" symbol:

```html
{:include; #/snippets.ntpl :}
```

When using "#" inside /path/to/tpl/template.ntpl, it becomes:

```html
{:include; /path/to/tpl/snippets.ntpl :}
```

In this way, we can create utilities without knowing the directory structure.

---
