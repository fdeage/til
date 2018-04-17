# CSS basic selectors

## Basics
- \*   all elements
- test  \<test>
- .test  \<div class='test'>   (shortcut for "[class=test]")
- \#test   is   \<div id='test'>        (shortcut for "[id=test]")


## Selectors (cf. [this](https://flukeout.github.io))
- h1 + p : all the \<p> right next to \</h1> (outside)
- h1    p : all the \<p> inside \<h1>...\</h1> (whatever the nesting level)
- h1 > p : all the \<p> inside and hierarchically right after \<h1> (a.k.a. first-generation child)
- h1 ,  p : all the \<p> or all the \<h1>
- h1    p : all the \<p> following \<h1> (whether inside or after)

Selectors are parsed right to left. The key selector is the right-most one: it should be as specific as possible (the worst being “#test * {}”)

The key selector is the one which determines just how much work the browser will have to do, so this is the one to keep an eye on.

("Performance is so interesting; it’s a weird balance between web standards best practices and sheer speed.")

At the opposite, an overqualified selector might look like:
"html body .wrapper #content a {}"
which forces the browser to do a lot of checks. It can probably be simplified in: "#content a {}"

## All pseudo-selectors
- :active
- :after
- :before
- :checked
- :disabled
- :empty
- :enabled
- :first-child
- :first-letter
- ::first-line
- :first-of-type
- :focus
- :hover
- :in-range
- :invalid
- :lang(language_code)
- :last-child
- :last-of-type
- :link
- :not(selector)
- :nth-child(n)
- :nth-last-child(n)
- :nth-last-of-type(n)
- :nth-of-type(n)
- :only-of-type
- :only-child
- :optional
- :out-of-range
- :read-only
- :read-write
- :required
- :root
- ::selection
- :target
- :valid
- :visited

(In cases where there is only one element, that element counts as the first-child, only-child and last-child)

## Default values for each HTML elements (cf. [W3S](https://www.w3schools.com/))
\<address>   defaults with "display: block; font-style: italic"
