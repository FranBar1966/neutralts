{:each; ... :}
==============

Iterate array.

```html
{:each; array keyname valuename >>
    code
:}

{:each; array-name key value >>
    {:;key:}={:;value:}
:}
```

Modifiers:
----------

```html
{:^each; ... :}
```

No flags
--------

Nesting
-------

Can be nested (no limit), the following iterates an array, for more levels to increase the nesting:

```html
{:^each; array key val >>
    {:array; val >>
        {:;:}
        {:;key:}:
        {:^each; val key val >>
            {:array; val >>
                {:;:}
                {:;key:}:
                {:^each; val key val >>
                    {:array; val >>
                        {:;:}
                        {:;key:}:
                        {:^each; val key val >>
                            {:;:}
                            {:;key:}={:;val:}
                        :}
                    :}{:else;
                        {:;:}
                        {:;key:}={:;val:}
                    :}
                :}
            :}{:else;
                {:;:}
                {:;key:}={:;val:}
            :}
        :}
    :}{:else;
        {:;:}
        {:;key:}={:;val:}
    :}
:}
```

For a recursive version of the above with no level limit, the following snippets could be set:

```html
{:snippet; iterate-array >>
    {:^each; {:param; array-name :} key value >>
        {:array; value >>
            {:;:}
            {:;key:}:
            {:snippet; iterate-array-next-level :}
        :}{:else;
            {:;:}
            {:;key:}={:;value:}
        :}
    :}
:}

{:snippet; iterate-array-next-level >>
    {:^each; value key value >>
        {:array; value >>
            {:;:}<br>
            {:;key:}:<br>
            {:snippet; iterate-array-next-level :}
        :}{:else;
            {:;:}<br>
            {:;key:}={:;value:}
        :}
    :}
:}
```

---
