This code is just a proof of concept illustrating how one could
support new constructs (including new keywords) in Python code.

Version 0
----------

This version contains a single file and was my starting point,
essentially what was the first
version used in Reeborg's World.  The file shows how one can
transform some source code so that
instances of

        repeat n:

where "n" evaluates as an integer, are replaced by

        for VAR_i in range(n):

Version 1
---------

This version contains 3 files.  One is the code converter, essentially
identical to the one file from the first version.  Another is a code sample
to be tested.  The third contains an "import hook".  The idea is that
when a module is imported, instead of the standard Python importer,
the custom "import hook" is first called and can decide to handle (and transform)
the code, or just pass it along to the standard Python importer.

Version 2
---------

This version is similar to the previous one.  The main change is that,
instead of having a hard-coded name for the code transformer, it is read
from the source code of the file to be imported.

Version 3
---------

This version handles multiple converters which can be chained.
The code for the converters has been changed from the original:
instead of some simple string substitutions, it uses the
tokenize module to perform changes.  This ensures that
code within comments (including docstrings) is unaffected which would
be useful to preserve docstrings used in Python's help().
