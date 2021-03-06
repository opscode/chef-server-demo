Chef-server demo
================

Overview
--------

Welcome to the Chef 11 Server Preview! This preview includes
[erchef](https://github.com/opscode/erchef/), the new Chef API server
written in Erlang.

This repository provides a `Vagrantfile` and installation cookbooks to
set up a self-contained vm running a complete Chef server environment
for your demo pleasure.

NOTE: This is a PREVIEW release. DO NOT RUN IN A PRODUCTION ENVIRONMENT.

Setting it up
-------------

In order to get started, you need to have a copy of the latest omnibus
generated preview `.deb` for chef-server. You can get this
[here](http://wiki.opscode.com/display/chef/Chef+11+Server+Preview). Then
follow these steps:

1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (exercise left to
   the reader). Next, install the required gems using bundler. Execute the following
   commands from inside the chef-server-demo directory.

       # install bundler if you don't already have it
       which bundle || gem install bundler

       # install the gems needed for chef-server-demo
       bundle install --binstubs
    
2. Copy the Chef server .deb [file](http://wiki.opscode.com) into the pkg
   sub-directory:

       curl -O $URL_FOR_CHEF_SERVER_DEB
       mv CHEF_SERVER.deb pkg/
    
3. Export environment variable `OSC_INSTALLER`, setting it to point at
   the omnibus installer .deb and provision your erchef powered Chef server:

       export OSC_INSTALLER=pkg/CHEF_SERVER.deb
       bin/vagrant up
    
Test Drive Time
---------------

You can log into your Chef server demo vm like this:

    bin/vagrant ssh

You can add the vagrant
[keys](https://github.com/mitchellh/vagrant/tree/master/keys) to your
SSH config to scp files out of the VM.

The `open-source-demo::default` recipe will have created a
`$HOME/.chef/knife.rb` for you so that you can start issuing knife
commands right away:

    knife client list
    export EDITOR=vi
    knife node create
    knife node list

The recipe also sets the `PATH` to include the command line tools for
the versions of postgres, rabbit, and erlang supplied in the omnibus
installer .deb. To get an overview of the Chef server system status
try this:

    sudo chef-server-ctl status

Controlling the server
-----------------------

There is a single init.d style control script `chef-server-ctl` which
controls all daemons used by the chef-server. This also provides the
ability to tail all the logs produced by the individual services. *Use
sudo or a root shell when using `chef-server-ctl`*.

    sudo chef-server-ctl  help


LICENSE
-------

Copyright 2012 Opscode, Inc. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License"); you may
not use this file except in compliance with the License. You may obtain
a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations
under the License.
