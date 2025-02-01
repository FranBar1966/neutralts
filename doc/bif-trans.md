{:trans; ... :}
===============

Translate a string.

```html
{:trans; String to translate :}
```

Modifiers
---------

```html
{:^trans; ... :}
{:!trans; ... :}
{:^!trans; ... :}
```
### Modifier: ^ (upline)

Eliminates previous whitespaces

Assuming that the translation of Hello is Hello:

```texplain
<div></div>

{:trans; Hello :}

<div></div>

{:^trans; Hello :}
```

Output:

```texplain
<div></div>

Hello

<div></div>Hello
```

### Modifier: ! (not)

By default the same string is output if there is no translation, to output an empty string use the modifier "not". Assuming there is no translation for "Hello".

```html
<div>{:trans; Hello :}</div>
<div>{:!trans; Hello :}</div>
<div>{:!trans; Hello :}{:else;
    There is no translation for "Hello".
:}</div>
```

Output:

```html
<div>Hello</div>
<div></div>
<div>There is no translation for "Hello".</div>
```

No flags
--------

References
----------

An APP can be created thinking that in the future it can be translated, we use in all the "trans" outputs;

```html
<ul>
    <li>{:trans; File :}</li>
    <li>{:trans; Edit :}</li>
</ul>
```

Simply add the translation without modifying the code.

We can also add a translation from the beginning and use the same or another strategy as references:

```html
<ul>
    <li>{:trans; ref:menu:file :}</li>
    <li>{:trans; ref:menu:edit :}</li>
</ul>

<ul>
    <li>{:trans; code:1002 :}</li>
    <li>{:trans; code:1003 :}</li>
</ul>
```

In this case it will be necessary to make sure that all references have a translation, or use "not" and "else":

```html
<li>{:!trans; ref:menu:edit :}{:else; Edit :}</li>
```

The "schema" takes care of the translation by means of the "locale" key of the scheme, the current language is defined with the "current" key:

```json
{
    "inherit": {
        "locale": {
            "current": "en"
            "trans": {
                "en": {
                    "Hello": "Hello",
                    "ref:greeting": "Hello"
                },
                "es": {
                    "Hello": "Hola",
                    "ref:greeting": "Hola"
                },
                "de": {
                    "Hello": "Hallo",
                    "ref:greeting": "Hallo"
                },
                "fr": {
                    "Hello": "Bonjour",
                    "ref:greeting": "Bonjour"
                }
            }
        }
    }
}
```

For more details see "schema" and "locale" bif.

Non-text translation
--------------------

The above strategies will work well for translating short text strings, but not for long text or even images.

We can use references to translate images:

```html
<img src="/images/cover-{:!trans; ref:lang :}{:else; english :}.jpg" />
```

For which we will need images with the appropriate file name:

```html
cover-english.jpg
cover-spanish.jpg
cover-french.jpg
```

With "else" we have set the default image, in case there is no translated image. Alternatively, we can do the following:

```html
<img src="/images/cover-{:!trans; ref:lang :}.jpg" />

cover-.jpg          // This is the default image
cover-english.jpg
cover-spanish.jpg
cover-french.jpg
```

And the corresponding translations in "locale":

```json
{
    "locale": {
        "trans": {
            "en": {
                "ref:lang": "english"
            },
            "en-us": {
                "ref:lang": "english"
            },
            "es": {
                "ref:lang": "spanish"
            },
            "es-es": {
                "ref:lang": "spanish"
            },
            "fr": {
                "ref:lang": "french"
            }
        }
    }
}
```

This same system will be useful for translating long texts using the same defined references:

```html
{:snippet; terms-conditions-{:!trans; ref:lang :}{:else; english :} :}
{:include; terms-conditions-{:!trans; ref:lang :}{:else; english :}.ntpl :}
```

Another strategy for translating images, long text and other content is the use of the “lang” bif which outputs the current language, first we define the snippet needed for each language, which can contain text, images, html, ...:

```html
{:snippet; contents-for-en >>
    ....
:}

{:snippet; contents-for-es >>
    ....
:}

{:snippet; contents-for-fr >>
    ....
:}
```

Then:

```html
{:snippet; contents-for-{:lang;:} :}{:else;
    {:snippet; contents-for-en :}
:}
```

A snippet that does not exist or is empty is not an error, but "else" detects it.

---