ABOUT
================

This "check_kumofs" is Nagios plugin for monitoring kumofs server node and manager node.

WHAT IS kumofs?
================

"kumofs" is a scalable and highly available distributed key-value store.

see also:
* [http://github.com/etolabo/kumofs#readme]
* [http://github.com/etolabo/kumofs/blob/master/doc/doc.en.md]
* [http://github.com/etolabo/kumofs]

INSTALLATION
================

    vi check_kumosvr
    vi check_kumosvr
      adjust path of kumostat or kumoctl to load
    cp check_kumo* /usr/local/bin/
      copy to where you like

EXAMPLE (Nagios)
================

commands.cfg
---------------

      define command {
        command_name  check_kumofs_server
        command_line  /usr/etolabo/bin/check_kumosvr $HOSTADDRESS$
      }
      define command {
        command_name  check_kumofs_manager
        command_line  /usr/etolabo/bin/check_kumomgr $HOSTADDRESS$ status
      }

hostgroup.cfg
----------------

      define hostgroup {
        hostgroup_name  kumofs_servers
        members         ks101, ks102, ks103, ks104, ks105, ks106
      }
      define hostgroup {
        hostgroup_name  kumofs_managers
        members         km101, km102
      }

services.cfg
----------------

      define service {
        use                  important-service
        hostgroup_name       kumofs_servers
        service_description  kumofs server health check
        check_command        check_kumofs_server
      }
      define service {
        use                  important-service
        hostgroup_name       kumofs_managers
        service_description  kumofs manager health check
        check_command        check_kumofs_manager
      }

SEE ALSO
================

check_memcached_paranoid
----------------
* [http://github.com/hirose31/nagios-check_memcached_paranoid]

check_memcached_paranodi is Nagios plugin for validating sequence of SET, GET, DELETE, GET by memcached protocol.


COPYRIGHT & LICENSE
================

Copyright (C) Etolabo Corp. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
