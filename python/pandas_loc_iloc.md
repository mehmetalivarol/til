Pandas has a few indexing functions available, and I can never get them straight.  

Pasting [some explanations](http://stackoverflow.com/questions/31593201/pandas-iloc-vs-ix-vs-loc-explanation) here to refer back to. 


+ **loc** works on labels in the index.
+ **iloc** works on the positions in the index (so it only takes integers).
+ **ix** usually tries to behave like loc but falls back to behaving like iloc if the label is not in the index.

It's important to note some subtleties that can make ix slightly tricky to use:

if the index is of integer type, ix will only use label-based indexing and not fall back to position-based indexing. If the label is not in the index, an error is raised.

if the index does not contain only integers, then given an integer, ix will immediately use position-based indexing rather than label-based indexing. If however ix is given another type (e.g. a string), it can use label-based indexing.
