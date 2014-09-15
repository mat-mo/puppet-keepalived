# puppet-keepalived

## Overview

Install, enable and configure the keepalived VRRP and LVS management daemon.

* `keepalived` : Main class to install, enable and configure the service.

The configuration file to be used can be specificed using either the `$content`
parameter (typically for templates), or the `$source` parameter. If neither is
specified, you will need to manage it rom elsewhere.

See the `templates/sysconfig.erb` file for the possible `$options` values. The
default is `-D` which enables both VRRP and LVS.

## Examples

Typical installation for VRRP only (no LVS), using a static existing
configuration file :

```puppet
class { '::keepalived':
  source  => "puppet:///${module_name}/keepalived.conf",
  options => '-D --vrrp',
}
```

Similar to the above, but using a template, which can be useful with multiple
servers which will be part of the same VRRP group and/or have the same LVS
configuration :

```puppet
class { '::keepalived':
  content => template("${module_name}/keepalived.conf.erb"),
}
```

