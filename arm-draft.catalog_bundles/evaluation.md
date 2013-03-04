Evaluation / Decision Support
=============================

* Does this reduce network communication?
* Is there the possibility of a strong default security model?
* Are possible workflows for handling puppet infrastructure and code expanded or contracted?

Disadvantages of a catalog bundle
---------------------------------

All of our existing infrastructure would need to be updated to handle a new way
of dealing with catalogs. This is no small undertaking.

There is a possibility that the catalog bundles get prohibitively large. There
is also a constant overhead of transfering data that may not be needed for the
catalog application because the file contents are in sync already.
