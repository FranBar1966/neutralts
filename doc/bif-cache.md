{:cache; ... :}
===============

Output code an store in cache. It is a modular cache with the option to exclude parts of the cache.

```html
{:cache; /expires/id/only_custom_id/ >> code :}
{:cache; /expires/id/ >> code :}
{:cache; /expires/ >> code :}
{:!cache; code :} {:* exclude from cache *:}
```

* expires: Seconds of life in the cache
* id: Add a literal to the cache ID
* only_custom_id: Use only the ID passed as ID,

The only mandatory parameter is `expires`, the cache automatically generates an ID with context data, such as language, cookies, ... and code.

With the `id` parameter you can add a literal to the ID that is automatically generated, or use just the `id` provided by adding a boolean true value to the third parameter:

```html
{:cache; /60/my-id/1/ >>
    {:code; foo :}
:}
```

The previous example replaces the automatic ID and this one adds:

```html
{:cache; /60/my-id/ >>
    {:code; foo :}
:}
```

Any delimiter can be used:

```html
{:cache; /expires/ >> ... :}
{:cache; ~expires~ >> ... :}
{:cache; #expires# >> ... :}
{:cache; |expires| >> ... :}
```

Example
--------

In this example the first date will be the same on every run for 300 seconds, the second date in the `!cache` block will not be included in the cache and will show a different date on every run.

```text
{:cache; /300/ >>
    <!DOCTYPE html>
    <html>
        <head>
            <title>Cache</title>
        </head>
        <body>
            <main>
                <div>In cache:{:date; %H:%M:%S :}</div>
                <div>No cache:{:!cache; {:date; %H:%M:%S :} :}</div>
            </main>
        </body>
    </html>
:}
```

With the cache ID a hash is generated and this will be the name of the file in the cache, by including the code in the hash each `cache` block with different code will generate a different cache file. This will generate two different caches without the need to specify additional ID:

```html
{:cache; /120/ >>
    {:code; foo :}
:}
{:cache; /120/ >>
    {:code; bar :}
:}
```

These two blocks of code being the same will have the same file in the cache:

```html
{:cache; /120/ >>
    {:code; foo :}
:}

...

{:cache; /120/ >>
    {:code; foo :}
:}
```

`expires` is included in the ID, so these two blocks of code are distinct:

```html
{:cache; /60/ >>
    {:code; foo :}
:}
{:cache; /120/ >>
    {:code; foo :}
:}
```

Modifiers:
----------

```html
{:^cache; ... :}
{:!cache; ... :}
```

### Modifier: ^ (upline)

Eliminates previous whitespaces, (See "unprintable" for examples.)

### Modifier: ! (not)

Excludes parts of the cache, the "bar" block is excluded from the cache:

```text
{:cache; /300/ >>
    {:code; foo :}
    {:!cache; {:code; bar :} :}
:}
```

You can use `!cache` outside a `cache` block to prevent that code from not being included in the cache in the future or by a parent:

```text
<!DOCTYPE html>
<html>
    <head>
        <title>Cache</title>
    </head>
    <body>
        <main>
            <div>{:!cache; {:code; foo :} :}</div>
        </main>
    </body>
</html>
```
No flags
--------

Nesting
-------

It can be nested, either `cache` or `!cache` or a mixture of both:

```text
{:cache; /20/ >>
    {:!cache;
        {:date; %H:%M:%S :}
        {:cache; /20/ >>
            {:!cache;
                {:date; %H:%M:%S :}
            :}
        :}
    :}
:}
```

Config
------

```text
{
    "config": {
        "cache_prefix": "neutral-cache",
        "cache_dir": "",
        "cache_on_post": false,
        "cache_on_get": true,
        "cache_on_cookies": true,
        "cache_disable": false
    },
    "inherit": {
        "locale": {
            "current": "en"
        }
    },
    "data": {
        "CONTEXT": {
            "ROUTE": "",
            "HOST": "",
            "GET": {},
            "POST": {},
            "HEADERS": {},
            "FILES": {},
            "COOKIES": {},
            "SESSION": {},
            "ENV": {}
        }
    }
}
```

The language is included in the cache ID, so there will always be different versions of the cache for each language, the language is defined in `inherit.locale.current`.

Various options can be set in the configuration:

* cache_prefix: Adds a prefix, one more level of cache directory.
* cache_dir: Directory where the cache files are stored, if empty, the temporary system directory.
* cache_on_post: Cache POST method, default false.
* cache_on_get: Cache GET method, default true.
* cache_on_cookies: Cache when cookies are present, default true.
* cache_disable: Completely disable the cache, default false.

When `cache_disable = false` on all values, possible bifs are filtered.

**In order for Neutral TS to detect POST, GET and cookies**, in your application you will have to **fill the `schema`** variable in `data` called **`CONTEXT`** with the POST, GET or cookie data.

Since POST requests are almost all different, it is useless to cache the POST method.

When GET or cookies are cached, different versions of the cache are generated for each variable or combination included in GET or cookies, using the automatic cache ID.


Examples
--------

If we run the following:

```text
{:cache; /300/ >>
    In cache: {:date; %S :}
    No cache: {:!cache; {:date; %S :} :}
:}
```

The first time will have the output:

```text
In cache: 30
No cache: 30
```

If we run it a second later, the `cache` part will be the same for 300 seconds, while the `!cache` part is always updated.

```text
In cache: 30
No cache: 31
```

Nesting:

```text
{:cache; /100/ >>
    {:date; %H:%M:%S :}
    {:cache; /300/ >>
        {:date; %H:%M:%S :}
        {:!cache; {:date; %H:%M:%S :} :}
    :}
:}
```

In the above example there is a global cache of 100 seconds and a nested cache of 300 seconds, the first date will be updated every 100 seconds and the second every 300 seconds. The last one in the `!cache` block will always be updated.

If the expiry of the nested cache were equal to or less than that of its parent, it would have no effect, they would be updated at the same time.

clean-cache
-----------

There is a bash utility here: [cache-utils](https://gitlab.com/neutralfw/neutralts/-/tree/master/cache-utils)  which can be run periodically to remove old cache files:

```text
clean-cache /tmp/neutral-cache
```

The parameter is the cache directory, for security reasons the directory must contain the text "neutral-cache" to avoid deleting things that are not in the cache, also only the subdirectories and files that have the Neutral TS format are deleted.

---
