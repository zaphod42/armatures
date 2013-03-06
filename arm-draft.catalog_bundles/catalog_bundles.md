Catalog Bundles
==========================

What is a catalog bundle?
-------------------------

Directory structure that contains:

````
  Metadata.json
  catalog.json
  index.json
  data/
  plugins/
````

These could be stored dumbly on disk or we can create a storage and de-dup
service much like puppetdb. By keeping this ARM agnostic as to the storage and
distrobution requirements, it leaves open that to many possibly implementations,
which allows the best system and workflow to be selected rather than imposing
anything.

Metadata.json
-------------

The Metadata.json file describes the contents of the bundle, the purpose is to provide
a standard way of specifying the origin, trustworthiness, and format of the rest of the data
contained in the bundle.

TODO: How should we handle signing of the contents?

### Format
````
  {
     bundle_format_version: *version_string // the catalog bundle format version
     bundle_id: *string   // arbitrary user specified identifier for the bundle

     compiled_by: *string
     compiled_on: *date

     bundled_by: *string
     bundled_on: *date

     approved_by: *string
     approved_on: *date
  }
````

Catalog.json
------------

The puppet catalog, which describes the resources

### Format

Either the existing catalog format, or perhaps the catalog format used by PuppetDB.
This is not yet determined.

Index.json and the data directory
----------

The `index.json` file is an index of the files found in the `data` directory. The index
also contains meta-information about the files, such as pre-computed checksums.

### Format

````
  {
    "<URI as referenced in the catalog>": {
      data: "<name of file located in data directory>",
      checksum: {
        value: "<checksum value in hex encoding>",
        type: Enum(md5, sha1, sha256)
      }
    },
    ...
  }
````

Plugins
-------

In order to make the catalog bundle self-contained, the bundle also needs to include the
plugins that will be needed in order to apply it. These are the types and providers referenced
by the catalog.
