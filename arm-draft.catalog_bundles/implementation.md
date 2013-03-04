Implementation
==============

Although there is nothing stopping us from keeping a service that
generates catalog bundles on the fly (like the current puppet master)
I think that in the long term moving away from that kind of model will
allow us a lot more flexibility, scalability, and easier maintenance.

Create a node artifact (takes the place of having an ENC later in the chain)
“puppet node generate nodename --facts facts.yaml --class class1 --class class2 --output nodename.node” 

Create a catalog bundle (takes all of the inputs: node, manifest, modules, data, catalog version)
“puppet catalog compile nodename.node --manifest env/site.pp --modulepath env/modules --output nodename.catalog --version 2.3.1”

Sign the bundle (catalog starts unsigned, approval process signs it)
“puppet catalog sign nodename.catalog --key mykey.pem”

Encrypt the catalog so that only the intended recipient can read it (metadata stays unencrypted)
"puppet catalog encrypt nodename.catalog --output nodename-encrypted.catalog --key nodename.pem"

Put in catalog repository
“puppet repo upload nodename.catalog”

Fetch from catalog repository (get by name and version)
“puppet repo download nodename --version 2.3.1 --output nodename-encrypted.catalog”

Decrypt the catalog
"puppet catalog decrypt nodename-encrypted.catalog --output nodename.catalog --key nodename-private.pem"

Apply the catalog
"puppet apply nodename.catalog"

This implementation is still underway.
