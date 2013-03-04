Spinoff
=======

Once catalog bundles are implemented there are a vast array of possible
extensions.

Catalog Diffing
---------------

Since a catalog bundle includes most of the pertinent information needed for
the application and understanding of a catalog, a diff of catalog bundles
provides a large amount of information about the changes that will be rolled
out.

Catalog Synchronization
-----------------------

Catalog bundles can potentially become very large. Even in the case in which
they are not large, the transfer of the bundle still takes bandwidth and time.
Systems could be created to transfer the bundles more efficiently (rsync, git,
bittorrent).

Catalog Encryption/Signing
--------------------------

The catalog bundle is an artifact that can be trusted. This is a departure from
the current model in which the communication channel is trusted. By trusting
the bundle there can be a separation between the creation of a catalog and the
application of it.  Various methods could be put in place for creating a
sign-off process, encryption standards, and so on.

Catalog Repository
------------------

Like many other artifact based systems, having a central repository of catalog
bundles, which are likely tied to version information, would be possible. This
would open the door for a history of configuration for a particular node or a
workflow based off of a new version becoming available.

Multi-node Catalogs
-------------------

The catalog bundle, as it currently is specified, allows for a single catalog
per node.  However, many nodes are nearly identical and might only differ by a
few values. Catalog bundles could be extended to have unresolved references to
node-local values, which would be resolved at application times. This would
allow for a single catalog bundle to apply to all nodes of a specific class.
