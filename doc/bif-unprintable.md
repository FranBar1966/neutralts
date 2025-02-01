{:;:} (unprintable)
===================

Output empty string, eliminates or preserves spaces.

```html
{:;:}
```

Modifiers
---------

```html
{:^;:}
```

### Modifier: ^ (upline)

Eliminates **previous** whitespaces.

Assuming varname = Hello:

```texplain
<div></div>

{:;varname:}

<div></div>

{:^;:}{:;varname:}
```

Output:

```texplain
<div></div>

Hello

<div></div>Hello
```

Assuming varname = Hello:

```texplain
-|
{:;:}

{:^;:}{:;varname:}
-|

{:^;:}{:;varname:}
```

Output:

```texplain
-|
Hello
-|Hello
```

No flags
--------

Usage
-----

The following are the same:

```textplain
<div>{:;:}</div>
<div>{:; :}</div>
<div>{:;     :}</div>
<div>{:;

:}</div>
```

Output:

```textplain
<div></div>
<div></div>
<div></div>
<div></div>
```

The usual behavior in output is as expected in practically all cases, the following produce the same output:

```textplain
<div>{:code;Hello:}</div>
<div>{:code; Hello :}</div>
<div>{:code;

    Hello

:}</div>
```

Output:

```textplain
<div>Hello</div>
<div>Hello</div>
<div>Hello</div>
```

But in special cases we may need to make it so that spaces or carriage returns are not removed. And this is the main use of unprintable Bif:

```textplain
<pre>
{:code;
    {:^;:}
    Hello
    {:^;:}
:}
</pre>
```

Output:

```textplain
<pre>
    Hello
</pre>
```

Preserve space:

```textplain
<div>{:code;   Hello   :}</div>
<div>{:code; {:;:} Hello :}</div>
<div> {:code; Hello :}</div>
```

Output:

```textplain
<div>Hello</div>
<div> Hello</div>
<div> Hello</div>
```


In the previous example:

```textplain
                  .--- preserve
                  |
                  v
<div>{:code; {:;:} Hello :}</div>

                  .--- preserve two
                  ||
                  vv
<div>{:code; {:;:}  Hello :}</div>
```


Not preserve spaces:

```textplain
<div>
    {:code;
        Hello
    :}
</div>
<div>{:;
    :}{:code;
        Hello
    :}{:;
:}</div>
```

Output:

```textplain
<div>
    Hello
</div>
<div>Hello</div>
```

---