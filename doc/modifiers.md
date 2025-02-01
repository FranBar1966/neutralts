modifiers
=========

Modifiers allow changing the behavior of the bif and each bif may or may not support a certain modifier:

```html
    ^ upline
    ! not
    + scope
```

Example:

```html
    {:^defined; varname >> ... :}
    {:!defined; varname >> ... :}
    {:+defined; varname >> ... :}
```

### Modifier: ^ (upline)

Eliminates previous whitespaces.

### Modifier: ! (not)

They usually negate, but may have less obvious behavior as in the case of bif trans.

```html
    {:defined; varname >> ... :}   {:* if varname is defined *:}
    {:!defined; varname >> ... :}  {:* if varname is not defined *:}

    {:trans; text :}               {:* translates the text or outputs text if no translation *:}
    {:!trans; text :}              {:* translates the text or outputs empty if no translation *:}

    {:exit; 302 :}                 {:* Terminate and set 302 status *:}
    {:!exit; 302 :}                {:* Set 302 status and continues executing *:}
```

### Modifier: + (scope)

By default the scope of the definitions is block inheritable to the children of the block:

```html
   {:code; <--------------------------.
       {:* block *:}                  |<---- Block
       {:param; name >> value :} <----|----- Set "name" for this block and its children
       {:param; name :} <-------------|----- "name" has the value "value".
       {:code;                        |
           {:* child block *:}        |
           {:param; name :} <---------|----- "name" has the value "value".
       :}                             |
   :} <-------------------------------·
   {:param; name :} <----------------------- outside block, no value or a previous value if any.
```

"include" has a block scope, then:

```html
   {:code;
       {:* include for set "snippet-name" *:}
       {:include; snippet.ntpl :}
       {:snippet; snippet-name :} {:* Ok, "snippet-name" is set *:}
   :}
   {:snippet; snippet-name :} {:* Ko, "snippet-name" is not set *:}
```

The modifier scope (+) adds the scope to the current level

```html
   {:+code;
       {:* include for set "snippet-name" *:}
       {:include; snippet.ntpl :}
       {:snippet; snippet-name :} {:* Ok, "snippet-name" is set *:}
   :}
   {:snippet; snippet-name :} {:* Ok, "snippet-name" is set *:}
```

To make it possible to do this:

```html
   {:bool; something >>
       {:include; snippet.ntpl :}
   :}
   {:snippet; snippet-name :} {:* Ko, "snippet-name" is not set *:}

   {:+bool; something >>
       {:include; snippet.ntpl :}
   :}
   {:snippet; snippet-name :} {:* Ok, "snippet-name" is set *:}
```

---