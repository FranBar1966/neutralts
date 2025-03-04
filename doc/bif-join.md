{:join; ... :}
==============

Output join array elements with a string.

```html
{:join; /array/literal/bool/ :}
{:join; /array/separator/keys/ :}
{:join; /array/separator/ :}
```

* array: an array
* separator: string as a separator
* keys: optional boolean for using keys instead of values, default false, values

Any delimiter can be used:

```html
{:join; ~array~separator~ :}
{:join; #array#separator# :}
{:join; |array|separator| :}
{:join; XarrayXseparatorX :}
```

Modifiers:
----------

```text
{:^join; ... :}
```

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

No flags
--------

Example
-------

```text
<li>{:join; |array|</li><li>| :}</li>
```

---
