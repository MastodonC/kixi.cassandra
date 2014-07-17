# Hecuba Docker

This project contains the files needed to create a Docker image through Vagrant, suitable for use with [Kixi.Hecuba](https://github.com/MastodonC/kixi.hecuba).
The included Dockerfile can be used to build an image of Ubuntu 14.04 running Cassandra 2.0.9.
Running the Vagrant file will build the Docker image, starting Cassandra in the image, and set port forwarding required to use cqlsh.

## Dev Environment

+ Install VirtualBox v4.3.8 from [here](https://www.virtualbox.org/wiki/Downloads) or preferably via your OS's package manager.
+ Install Vagrant v. 1.4.3 from [here](http://www.vagrantup.com/) or preferably via your OS's package manager.
+ install the vbguest plugin so Virtual Box guest additions will updated
  for you ``vagrant plugin install vagrant-vbguest``
+ ``cd ${PROJECT_HOME}``
+ ``vagrant up`` (The first time it is run, this will download a base image of Ubuntu 14.04 from Docker and then install the required packages on the image. So it will be slow the first time, but after that it will be a lot quicker)
+ You will now have all the services required running in a virtual machine with the ports forwarded for access from your local machine

## Usage with Kixi.Hecuba

+ ``cd`` to ``kixi.hecuba/cql``
+ ``cqlsh -f hecuba-schema.cql``
+ Start a repl in your favourite way.
+ Start kixi.hecuba with ``(go)``
+ ``(require 'etl)``
+ ``(kixi.hecuba.security/add-user! (:store system) "someone@example.com" "<password>" #{:kixi.hecuba.security/super-admin})`` (the username and password should match those in .hecuba.edn
+ ``(etl/load-test-data system)``
+ Then view localhost:8010 in a browser

## License

Copyright © 2014 Mastodon C Ltd

Distributed under the Eclipse Public License version 1.0.

