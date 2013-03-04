Alternatives
============

Why this and not the static compiler?
-------------------------------------

The static compiler tries to create a versionable catalog by replacing all file
references with a digest of the contents. It then places the contents of that
file in a file bucket at the time of compilation. The file bucket system is
part of a specific puppet master, which means that load balancing the puppet
master becomes more difficult. The current implementation of the static
compiler also ends up reading the entire file contents into memory, computing
the digest and writing the file contents back out to another location. That is
not an insurmountable problem (we need to work with streams of data instead of
all data in memeory at once), but is a problem nonetheless.

Another problem with the static compiler is that it creates an artifact that is
not complete. Without the filebucket the catalog is incomplete since no review
process is reliable without being able to access the contents stored in the
filebucket. There is also no information in the system about when a file in the
filebucket can be removed. There may still be an agent with a cached catalog
that will want to query that file in the future.

The static compiler offers two improvements over the existing catalog:

  1. There is no metadata request to the master required for the agent to discover if a file is out of date
  2. A catalog diff can provide the information that the file contents have changed between catalog versions (although not what the change was)

A catalog bundle can provide both of those improvements as well, plus provides
the information about what changed in the contents. The number of network
requests needed for a catalog bundle is just 1, the single request needed to
get the bundle.

The workflow that I envision for a catalog bundle separate the creation of a
catalog from an agent's request for a catalog. This would provide the user much
more control over the process of pushing changes to their infrastructure. Part
of this is the fact that with all of the data included in the bundle, a review
process can be a workflow of artifact promotion of disconnected systems where the
interaction is done only via transfer of a bundle from one stage to the next. This
is truly SOA.
