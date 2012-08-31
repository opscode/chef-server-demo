
Chef-server demo
================

Overview
--------

Welcome to a preview of Chef 11! This preview includes erchef,
the new Chef API server written in Erlang. This repository contains
a `Vagrantfile` and installation cookbooks to set up a self-contained
vm running a complete Chef server environment for your demo pleasure.

Setting it up
-------------

In order to get started you need to have a copy of the latest omnibus
generated `.deb` for chef-server.  You can get this [here](). Copy the
`.deb` into a location that is shared with the VM and starting vagrant.

1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (exercise left to
   the reader). Next, install the required gems using bundler. Execute the following
   commands from inside the chef-server-demo directory.

```
    which bundle || gem install bundler
```

```
    bundle install --binstubs
```

2. Copy the Chef server .deb [file](http://wiki.opscode.com) into the pkg
   sub-directory:

```
    curl -O $URL_FOR_CHEF_SERVER_DEB
```

```
    mv chef-server.deb pkg/
```

3. Export environment variable `OSC_INSTALLER`, setting it to point at
   the omnibus installer .deb and provision your Erchef powered Chef server:

```
   export OSC_INSTALLER=pkg/CHEF_SERVER.deb
```

```
    bin/vagrant up
```

Once the vagrant run is finished, the vagrant box will be set up and open source
chef server will be running.  If there are any errors, they should be visible in
the output from the vagrant up command.

The `open-source-demo::default` recipe also sets up the `PATH` on the virtual machine
the add the command line tools for the versions of postgres, rabbit, erlang supplied in
the omnibus installer .deb. It also sets up a knife.rb for the vagrant user in `$HOME/.chef`.
You can use the `vagrant ssh` command to log into the running VM. You'll need to add
the vagrant [keys](https://github.com/mitchellh/vagrant/tree/master/keys) to your SSH config to scp
files out of the VM.

You should now be able to try out knife commands against the server.

Controlling the server
-----------------------

There is a single init.d style control script `chef-server-ctl` which
controls all daemons used by the chef-server. This also provides the
ability to tail all the logs produced by the individual services. Use
sudo or a root shell when using `chef-server-ctl`.

    # chef-server-ctl  help
    /opt/chef-server/embedded/bin/omnibus-ctl: command (subcommand)
    cleanse
      Delete *all* private chef data, and start from scratch.
    graceful-kill
      Attempt a graceful stop, then SIGKILL the entire process group.
    help
      Print this help message.
    hup
      Send the services a HUP.
    int
      Send the services an INT.
    kill
      Send the services a KILL.
    once
      Start the services if they are down. Do not restart them if they stop.
    reconfigure
      Reconfigure the application.
    restart
      Stop the services if they are running, then start them again.
    service-list
      List all the services (enabled services appear with a *.)
    show-config
      Show the configuration that would be generated by reconfigure.
    start
      Start services if they are down, and restart them if they stop.
    status
      Show the status of all the services.
    stop
      Stop the services, and do not restart them.
    tail
      Watch the service logs of all enabled services.
    term
      Send the services a TERM.
    test
      Run the API test suite against localhost.
    uninstall
      Kill all processes and uninstall the process supervisor (data will be
      preserved).

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
See the License for the specific language governing permissions and
Chef-server demo
================

Overview
--------

Welcome to Erchef, the new Erlang based Chef server. This
repository contains a `Vagrantfile` and installation cookbooks to
set up a self-contained vm running a complete Chef server environment
for your demo pleasure.

Setting it up
-------------

In order to get started you need to have a copy of the latest omnibus
generated `.deb` for chef-server.  You can get this [here](). Copy the
`.deb` into a location that is shared with the VM and starting vagrant.

1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (exercise left to
   the reader). Next, install the required gems using bundler. Execute the following
   commands from inside the chef-server-demo directory.
```
    which bundle || gem install bundler

    bundle install --binstubs
```

2. Copy the [Chef server omnibus .deb][] into the pkg
   sub-directory:
```
    curl -O $URL_FOR_CHEF_SERVER_DEB

    mv chef-server.deb pkg/
```

3. Export environment variable `OSC_INSTALLER`, setting it to point at
   the omnibus installer .deb and provision your Erchef powered Chef server:

```
    > export OSC\_INSTALLER=pkg/chef-server_0.10.8-198-g6d59524-1.ubuntu.10.04_amd64.deb

    > bin/vagrant up
```

Test drive time
---------------

The `open-source-demo::default` recipe also sets up the `PATH` on the virtual machine
the add the command line tools for the versions of postgres, rabbit, erlang supplied in
the omnibus installer .deb. It also sets up a knife.rb for the vagrant user in `$HOME/.chef`.
You can use the `vagrant ssh` command to log into the running VM.

You should now be able to try out knife commands against the server.
=======
You can log into your Chef server demo vm like this:

    bin/vagrant ssh

You'll need to add the vagrant [keys](https://github.com/mitchellh/vagrant/tree/master/keys) to
your local SSH config if you want to scp files out of the VM.

The `open-source-demo::default` recipe will have created a
`$HOME/.chef/knife.rb` for you so that you can start issueing knife
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
See the License for the specific language governing permissions and
