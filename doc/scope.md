Scope and inheritance
=====================

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
