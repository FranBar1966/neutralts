{:contains; ... :}
==================

Output code if contains.

```html
{:contains; /literal/literal/ >> code :}
{:contains; /haystack/needle/ >> code :}
{:contains; /{:;varname:}/42/ >> ... :}
```
Any delimiter can be used:

```html
{:contains; ~haystack~needle~ >> ... :}
{:contains; #haystack#needle# >> ... :}
{:contains; |haystack|needle| >> ... :}
{:contains; XhaystackXneedleX >> ... :}
...
```

Modifiers:
----------

```text
{:^contains; ... :}
{:!contains; ... :}
```

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

### Modifier: ! (not)

```text
{:!contains; /haystack/needle/ >> this shown if is not contains. :}
```

No flags
--------

---
