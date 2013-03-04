Catalog Bundles
==========================

What is a catalog bundle?
-------------------------

Tar file that contains:
  Metadata.json
  data.tar.gz

Metadata.json:

````
  {
     bundle_format_version: *version_string // the catalog bundle format version
     bundle_id: *string   // arbitrary user specified identifier for the bundle
     authority: *string   // public certificate of the signer of the content 
                          // (do we need the whole thing?)
     signiture: *string   // cryptographic signiture of the data.tar.gz file
     certificate: *string // the public certificate of the owner of the data.tar.gz
                          // (the node's public certificate) (do we need the whole thing?)
     encrypted: *boolean  // whether the data.tar.gz file has been encrypted using
                          // the certificate
     compiled_by: *string
     compiled_on: *date

     bundled_by: *string
     bundled_on: *date

     approved_by: *string
     approved_on: *date
  }
````

data.tar.gz
````
  catalog.json  // the catalog graph (format used by puppetdb? probably)
  lib/          // dir of the extra code that the agent will need in order
                // to apply the catalog (equivalent of the pluginsync)
  data/         // dir of the file contents referenced by the catalog
    \-> <digest of file contents> // the file contents. Each file is named 
                                  // as the digest of the contents and contains
                                  // simply the desired file contents
````

These could be stored dumbly on disk or we can create a storage and de-dup
service much like puppetdb. In the case of the service, they would have to be
submitted unencryped and when they are requested they are possibly encrypted at
that time (TLS would be enough by that point). The encryption option is mainly
to support being able to hand around a catalog safely.
