.. _js-style:

JS Style Guide
==============

First and Foremost
------------------

**ALWAYS** use JSHint_ on your code.

.. Note::

   There are some exceptions for which JSHint complains about things in node
   that you can ignore, like how it doesn't know what 'const' is and complains
   about not knowing what 'require' is. You can add keywords to ignore to a
   `.jshintrc` file.

.. _JSHint: http://jshint.com/


Variable Formatting:
--------------------

::

    // Classes: CapitalizedWords
    var MyClass = ...

    // Variables and Functions: camelCase
    var myVariable = ...

    // Constants: UPPER_CASE_WITH_UNDERSCORES
    // Backend
    const MY_CONST = ...

    // Client-side
    var MY_CONST = ...


Indentation
~~~~~~~~~~~

4-space indents (no tabs).

For our projects, always assign var on a newline, not comma separated::

    // Bad
    var a = 1,
        b = 2,
        c = 3;

    // Good
    var a = 1;
    var b = 2;
    var c = 3;


Use ``[]`` to assign a new array, not ``new Array()``.

Use ``{}`` for new objects, as well.

Two scenarios for ``[]`` (one can be on the same line, with discretion
and the other not so much)::

    // Okay on a single line
    var stuff = [1, 2, 3];

    // Never on a single line, multiple only
    var longerStuff = [
        'some longer stuff',
        'other longer stuff'
    ];


Never assign multiple variables on the same line
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bad::

    var a = 1, b = 'foo', c = 'wtf';


DO NOT line up variable names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bad::

    var wut    = true;
    var boohoo = false;


Semicolons
-----------

**Use them.**

Not because ASI is black magic, or whatever. I'm sure we all understand ASI.
Just do it for consistency.


Conditionals and Loops
----------------------

::

    // Bad
    if (something) doStuff()

    // Good
    if (something) {
        doStuff();
    }


Space after keyword, and space before curly
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    // Bad
    if(bad){

    }

    // Good
    if (something) {

    }


Functions
---------

.. _named-functions:

Named Functions
~~~~~~~~~~~~~~~

There's no need to explicitly name a function when you're already
assigning it to a descriptively named symbol::

    var updateOnClick = function() { ... };

...or... ::

    var someObject = {updateOnClick: function() { ... }

Most modern JS engines will infer the name *updateOnClick* for the above
anonymous function and use it in tracebacks.

Of course, if you're passing a nontrivial function as an argument, you
should still contrive to name it somehow. The meaning here would be
needlessly obscured if the anonymous function were, for example, 10 lines long::

    .forEach(function() { ... })

In such cases, either name the function, or pass a descriptively named
symbol that points to a function.


Whitespacing Functions
~~~~~~~~~~~~~~~~~~~~~~

No space between name and opening paren. Space between closing paren and brace::

    var method = function(argOne, argTwo) {

    };


Anonymous Functions
~~~~~~~~~~~~~~~~~~~

Anonymous functions are fine if they have a small amount of code in them. See
the :ref:`named-functions` section for info about inferred function names for
anonymous functions.


Operators
---------

Always use ``===``.

Only exception is when testing for null and undefined.

Example::

    if (value != null) {

    }


Quotes
------

Always use single quotes: ``'not double'``

Only exception: ``"don't escape single quotes in strings. use double quotes"``


Comments
--------

For node functions, always provide a clear comment in this format::

    /* Briefly explains what this does
     * Expects: whatever parameters
     * Returns: whatever it returns
     */


If comments are really long, also do it in the ``/* ... */`` format like above.
Otherwise make short comments like::

    // This is my short comment and it ends in a period.


Ternaries
---------

Try not to use them.

If a ternary uses multiple lines, don't use a ternary::

    // Bad
    var foo = (user.lastLogin > new Date().getTime() - 16000) ? user.lastLogin - 24000 : 'wut';

    // Good
    return user.isLoggedIn ? 'yay' : 'boo';


General Good Practices
----------------------

If you see yourself repeating something that can be a constant, refactor it as a
single constant declaration at the top of the file.

Cache regex into a constant.

Always check for truthiness::

    // Bad
    if (blah !== false) { ...

    // Good
    if (blah) { ...


If code is really long, try to break it up to the next line or refactor (try to
keep within the 80-col limit but if you go a bit past it's not a big deal).
Indent the subsequent lines one indent (2-spaces) in.

If it looks too clever, it probably is, so just make it simple.
