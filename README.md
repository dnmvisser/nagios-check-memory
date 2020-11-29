# nagios-check-memory

Adapted verion of the `/usr/lib/nagios/plugins/check_memory` plugin from the
`nagios-plugins-contrib` package.

It takes into account any ballooned memory when the
`/usr/bin/vmware-toolbox-cmd` script is available. This is memory that is eated
up by the VMware Balloon driver, so it is reported by `free` as "used".
See
https://community.microfocus.com/t5/Access-Manager-Tips-Information/How-VMWare-ESX-and-ESXi-Memory-Ballooning-impacts-Access-Manager/ta-p/1776771.

So on VMware guests, monitoring the amount of memory using the output of `free`
will give false alarms. To overcome that, this version checks the amount of
ballooned memory by running `vmware-toolbox-cmd stat balloon`, and will add that
to the amount of free memory. This will return more realistic results, and
prevent false alarms.

