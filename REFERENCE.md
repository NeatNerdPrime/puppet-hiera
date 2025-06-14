# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

#### Public Classes

* [`hiera`](#hiera): This class handles installing the hiera.yaml for Puppet's use. Creates either /etc/puppet/hiera.yaml or /etc/puppetlabs/puppet/hiera.yaml in set hiera version and links /etc/hiera.yaml to it. Creates $datadir (if $datadir_manage == true).
* [`hiera::deep_merge`](#hiera--deep_merge): This class installs and configures deep_merge
* [`hiera::eyaml_gpg`](#hiera--eyaml_gpg): This calls install and configures hiera-eyaml-gpg
* [`hiera::params`](#hiera--params): This class handles OS-specific configuration of the hiera module. It looks for variables in top scope (probably from an ENC such as Dashboard). If the variable doesn't exist in top scope, it falls back to a hard coded default value.

#### Private Classes

* `hiera::eyaml`: This class installs and configures hiera-eyaml

### Defined types

#### Private Defined types

* `hiera::install`: Private define

### Data types

* [`Hiera::Hiera5_defaults`](#Hiera--Hiera5_defaults): This will validate hiera 5 'defaults' hash
* [`Hiera::Hiera5_hierarchy`](#Hiera--Hiera5_hierarchy): This will validate hiera 5 hierarchy array hash

## Classes

### <a name="hiera"></a>`hiera`

=== Copyright:

Copyright (C) 2012 Hunter Haugen, unless otherwise noted.
Copyright (C) 2013 Mike Arnold, unless otherwise noted.
Copyright (C) 2014 Terri Haber, unless otherwise noted.
Copyright (C) 2016 Vox Pupuli, unless otherwise noted.

#### Parameters

The following parameters are available in the `hiera` class:

* [`hierarchy`](#-hiera--hierarchy)
* [`hiera_version`](#-hiera--hiera_version)
* [`hiera5_defaults`](#-hiera--hiera5_defaults)
* [`backends`](#-hiera--backends)
* [`backend_options`](#-hiera--backend_options)
* [`hiera_yaml`](#-hiera--hiera_yaml)
* [`create_symlink`](#-hiera--create_symlink)
* [`datadir`](#-hiera--datadir)
* [`datadir_manage`](#-hiera--datadir_manage)
* [`owner`](#-hiera--owner)
* [`group`](#-hiera--group)
* [`mode`](#-hiera--mode)
* [`eyaml_owner`](#-hiera--eyaml_owner)
* [`eyaml_group`](#-hiera--eyaml_group)
* [`provider`](#-hiera--provider)
* [`eyaml`](#-hiera--eyaml)
* [`eyaml_name`](#-hiera--eyaml_name)
* [`eyaml_version`](#-hiera--eyaml_version)
* [`eyaml_source`](#-hiera--eyaml_source)
* [`eyaml_datadir`](#-hiera--eyaml_datadir)
* [`eyaml_extension`](#-hiera--eyaml_extension)
* [`confdir`](#-hiera--confdir)
* [`puppet_conf_manage`](#-hiera--puppet_conf_manage)
* [`logger`](#-hiera--logger)
* [`cmdpath`](#-hiera--cmdpath)
* [`create_keys`](#-hiera--create_keys)
* [`keysdir`](#-hiera--keysdir)
* [`deep_merge_name`](#-hiera--deep_merge_name)
* [`deep_merge_version`](#-hiera--deep_merge_version)
* [`deep_merge_source`](#-hiera--deep_merge_source)
* [`deep_merge_options`](#-hiera--deep_merge_options)
* [`merge_behavior`](#-hiera--merge_behavior)
* [`extra_config`](#-hiera--extra_config)
* [`master_service`](#-hiera--master_service)
* [`manage_package`](#-hiera--manage_package)
* [`manage_eyaml_package`](#-hiera--manage_eyaml_package)
* [`manage_deep_merge_package`](#-hiera--manage_deep_merge_package)
* [`manage_eyaml_gpg_package`](#-hiera--manage_eyaml_gpg_package)
* [`package_name`](#-hiera--package_name)
* [`package_ensure`](#-hiera--package_ensure)
* [`eyaml_gpg_name`](#-hiera--eyaml_gpg_name)
* [`eyaml_gpg_version`](#-hiera--eyaml_gpg_version)
* [`eyaml_gpg_source`](#-hiera--eyaml_gpg_source)
* [`eyaml_gpg`](#-hiera--eyaml_gpg)
* [`eyaml_gpg_gnupghome_recurse`](#-hiera--eyaml_gpg_gnupghome_recurse)
* [`eyaml_gpg_recipients`](#-hiera--eyaml_gpg_recipients)
* [`eyaml_pkcs7_private_key`](#-hiera--eyaml_pkcs7_private_key)
* [`eyaml_pkcs7_public_key`](#-hiera--eyaml_pkcs7_public_key)
* [`ruby_gpg_name`](#-hiera--ruby_gpg_name)
* [`ruby_gpg_version`](#-hiera--ruby_gpg_version)
* [`ruby_gpg_source`](#-hiera--ruby_gpg_source)
* [`gem_install_options`](#-hiera--gem_install_options)
* [`gem_source`](#-hiera--gem_source)

##### <a name="-hiera--hierarchy"></a>`hierarchy`

Data type: `Variant[Array, Array[Hash]]`

The hiera hierarchy.

Default value: `$hiera::params::hierarchy`

##### <a name="-hiera--hiera_version"></a>`hiera_version`

Data type: `Optional[Enum['3','5']]`

To set hiera 5 defaults. e.g. datadir, data_hash.

Default value: `$hiera::params::hiera_version`

##### <a name="-hiera--hiera5_defaults"></a>`hiera5_defaults`

Data type: `Hiera::Hiera5_defaults`

Version format to layout hiera.yaml. Should be a string.

Default value: `$hiera::params::hiera5_defaults`

##### <a name="-hiera--backends"></a>`backends`

Data type: `Any`

The list of backends. If you supply a additional backend you must also supply the backend data in the backend_options hash.

Default value: `['yaml']`

##### <a name="-hiera--backend_options"></a>`backend_options`

Data type: `Any`

An optional hash of backend data for any backend. Each key in the hash should be the name of the backend as listed in the backends array. You can also supply additional settings for the backend by passing in a hash. By default the yaml and eyaml backend data will be added if you enable them via their respective parameters. Any options you supply for yaml and eyaml backend types will always override other parameters supplied to the hiera class for that backend.

Example hiera data for the backend_options hash:

```
backend_options:
  json:
    datadir: '/etc/puppetlabs/puppet/%{environment}/jsondata'
  redis:
    password: clearp@ssw0rd        # if your Redis server requires authentication
    port: 6380                     # unless present, defaults to 6379
    db: 1                          # unless present, defaults to 0
    host: db.example.com           # unless present, defaults to localhost
    path: /tmp/redis.sock          # overrides port if unixsocket exists
    soft_connection_failure: true  # bypass exception if Redis server is unavailable; default is false
    separator: /                   # unless present, defaults to :
    deserialize: :json             # Try to deserialize; both :yaml and :json are supported
```

NOTE: The backend_options must not contain symbols as keys ie :json: despite the hiera config needing symbols. The template will perform all the conversions to symbols in order for hiera to be happy. Because puppet does not use symbols there are minor annoyances when converting back and forth and merge data together.

Default value: `{}`

##### <a name="-hiera--hiera_yaml"></a>`hiera_yaml`

Data type: `Any`

The path to the hiera config file. Note: Due to a bug, hiera.yaml is not placed in the codedir. Your puppet.conf hiera_config setting must match the configured value; see also hiera::puppet_conf_manage

Default value: `$hiera::params::hiera_yaml`

##### <a name="-hiera--create_symlink"></a>`create_symlink`

Data type: `Any`

Whether to create the symlink /etc/hiera.yaml

Default value: `true`

##### <a name="-hiera--datadir"></a>`datadir`

Data type: `Any`

The path to the directory where hiera will look for databases.

Default value: `$hiera::params::datadir`

##### <a name="-hiera--datadir_manage"></a>`datadir_manage`

Data type: `Any`

Whether to create and manage the datadir as a file resource.

Default value: `true`

##### <a name="-hiera--owner"></a>`owner`

Data type: `Any`

The owner of managed files and directories.

Default value: `$hiera::params::owner`

##### <a name="-hiera--group"></a>`group`

Data type: `Any`

The group owner of managed files and directories.

Default value: `$hiera::params::group`

##### <a name="-hiera--mode"></a>`mode`

Data type: `Any`



Default value: `$hiera::params::mode`

##### <a name="-hiera--eyaml_owner"></a>`eyaml_owner`

Data type: `Any`



Default value: `$hiera::params::eyaml_owner`

##### <a name="-hiera--eyaml_group"></a>`eyaml_group`

Data type: `Any`



Default value: `$hiera::params::eyaml_group`

##### <a name="-hiera--provider"></a>`provider`

Data type: `Any`

Which provider to use to install hiera-eyaml. Can be:
  puppetserver_gem (PE 2015.x or FOSS using puppetserver)
  pe_puppetserver_gem (PE 3.7 or 3.8)
  pe_gem (PE pre-3.7)
  puppet_gem (agent-only gem)
  gem (FOSS using system ruby (ie puppetmaster)) Note: this module cannot detect FOSS puppetserver and you must pass provider => 'puppetserver_gem' for that to work. See also master_service.

Default value: `$hiera::params::provider`

##### <a name="-hiera--eyaml"></a>`eyaml`

Data type: `Any`

Whether to install, configure, and enable the eyaml backend. Also see the provider and master_service parameters.

Default value: `false`

##### <a name="-hiera--eyaml_name"></a>`eyaml_name`

Data type: `Any`

The name of the eyaml gem.

Default value: `'hiera-eyaml'`

##### <a name="-hiera--eyaml_version"></a>`eyaml_version`

Data type: `Any`

The version of hiera-eyaml to install. Accepts 'installed', 'latest', '2.0.7', etc

Default value: `undef`

##### <a name="-hiera--eyaml_source"></a>`eyaml_source`

Data type: `Any`

An alternate gem source for installing hiera-eyaml.

Default value: `undef`

##### <a name="-hiera--eyaml_datadir"></a>`eyaml_datadir`

Data type: `Any`

The path to the directory where hiera will look for databases with the eyaml backend.

Default value: `undef`

##### <a name="-hiera--eyaml_extension"></a>`eyaml_extension`

Data type: `Any`

The file extension for the eyaml backend.

Default value: `undef`

##### <a name="-hiera--confdir"></a>`confdir`

Data type: `Any`

The path to Puppet's confdir.

Default value: `$hiera::params::confdir`

##### <a name="-hiera--puppet_conf_manage"></a>`puppet_conf_manage`

Data type: `Any`

Whether to manage the puppet.conf hiera_config value or not.

Default value: `true`

##### <a name="-hiera--logger"></a>`logger`

Data type: `Any`

Which hiera logger to use. Note: You need to manage any package/gem dependencies yourself.

Default value: `'console'`

##### <a name="-hiera--cmdpath"></a>`cmdpath`

Data type: `Any`

Search paths for command binaries, like the eyaml command. The default should cover most cases.

Default value: `$hiera::params::cmdpath`

##### <a name="-hiera--create_keys"></a>`create_keys`

Data type: `Any`

Whether to create pkcs7 keys and manage key files for hiera-eyaml. This is useful if you need to distribute a pkcs7 key pair.

Default value: `true`

##### <a name="-hiera--keysdir"></a>`keysdir`

Data type: `Any`

Directory for hiera to manage for eyaml keys. Note: If using PE 2013.x+ and code-manager set the keysdir under the $confdir/code-staging directory to allow the code manager to sync the keys to all PuppetServers Example: /etc/puppetlabs/code-staging/keys

Default value: `undef`

##### <a name="-hiera--deep_merge_name"></a>`deep_merge_name`

Data type: `Any`

The name of the deep_merge gem.

Default value: `'deep_merge'`

##### <a name="-hiera--deep_merge_version"></a>`deep_merge_version`

Data type: `Any`

The version of deep_merge to install. Accepts 'installed', 'latest', '2.0.7', etc.

Default value: `undef`

##### <a name="-hiera--deep_merge_source"></a>`deep_merge_source`

Data type: `Any`

An alternate gem source for installing deep_merge.

Default value: `undef`

##### <a name="-hiera--deep_merge_options"></a>`deep_merge_options`

Data type: `Any`

A hash of options to set in hiera.yaml for the deep merge behavior.

Default value: `{}`

##### <a name="-hiera--merge_behavior"></a>`merge_behavior`

Data type: `Any`

Which hiera merge behavior to use. Valid values are 'native', 'deep', and 'deeper'. Deep and deeper values will install the deep_merge gem into the puppet runtime.

Default value: `undef`

##### <a name="-hiera--extra_config"></a>`extra_config`

Data type: `Any`

Arbitrary YAML content to append to the end of the hiera.yaml config file. This is useful for configuring backend-specific parameters.

Default value: `''`

##### <a name="-hiera--master_service"></a>`master_service`

Data type: `Any`

The service name of the master to restart after package installation or hiera.yaml changes. Note: You must pass master_service => 'puppetserver' for FOSS puppetserver

Default value: `$hiera::params::master_service`

##### <a name="-hiera--manage_package"></a>`manage_package`

Data type: `Any`

A boolean for wether the hiera package should be managed.

Default value: `$hiera::params::manage_package`

##### <a name="-hiera--manage_eyaml_package"></a>`manage_eyaml_package`

Data type: `Boolean`



Default value: `true`

##### <a name="-hiera--manage_deep_merge_package"></a>`manage_deep_merge_package`

Data type: `Boolean`



Default value: `true`

##### <a name="-hiera--manage_eyaml_gpg_package"></a>`manage_eyaml_gpg_package`

Data type: `Boolean`



Default value: `true`

##### <a name="-hiera--package_name"></a>`package_name`

Data type: `Any`

Specifies the name of the hiera package.

Default value: `$hiera::params::package_name`

##### <a name="-hiera--package_ensure"></a>`package_ensure`

Data type: `Any`

Specifies the ensure value of the hiera package.

Default value: `$hiera::params::package_ensure`

##### <a name="-hiera--eyaml_gpg_name"></a>`eyaml_gpg_name`

Data type: `Any`



Default value: `'hiera-eyaml-gpg'`

##### <a name="-hiera--eyaml_gpg_version"></a>`eyaml_gpg_version`

Data type: `Any`



Default value: `undef`

##### <a name="-hiera--eyaml_gpg_source"></a>`eyaml_gpg_source`

Data type: `Any`



Default value: `undef`

##### <a name="-hiera--eyaml_gpg"></a>`eyaml_gpg`

Data type: `Any`



Default value: `false`

##### <a name="-hiera--eyaml_gpg_gnupghome_recurse"></a>`eyaml_gpg_gnupghome_recurse`

Data type: `Boolean`

Whether to recurse and set permissions in the gpgdir. This is imporant to protect the key, but makes puppet agent raise an error on each run. You can set the mode on these files to 0600 by yourself and set this to false.

Default value: `true`

##### <a name="-hiera--eyaml_gpg_recipients"></a>`eyaml_gpg_recipients`

Data type: `Any`



Default value: `undef`

##### <a name="-hiera--eyaml_pkcs7_private_key"></a>`eyaml_pkcs7_private_key`

Data type: `Any`



Default value: `undef`

##### <a name="-hiera--eyaml_pkcs7_public_key"></a>`eyaml_pkcs7_public_key`

Data type: `Any`



Default value: `undef`

##### <a name="-hiera--ruby_gpg_name"></a>`ruby_gpg_name`

Data type: `Any`



Default value: `'ruby_gpg'`

##### <a name="-hiera--ruby_gpg_version"></a>`ruby_gpg_version`

Data type: `Any`



Default value: `undef`

##### <a name="-hiera--ruby_gpg_source"></a>`ruby_gpg_source`

Data type: `Any`



Default value: `undef`

##### <a name="-hiera--gem_install_options"></a>`gem_install_options`

Data type: `Optional[Array]`

An array of install options to pass to the gem package resources. Typically, this parameter is used to specify a proxy server. eg gem_install_options => ['--http-proxy', 'http://proxy.example.com:3128']

Default value: `undef`

##### <a name="-hiera--gem_source"></a>`gem_source`

Data type: `Any`



Default value: `undef`

### <a name="hiera--deep_merge"></a>`hiera::deep_merge`

=== Copyright:

Copyright (C) 2016 Joseph Yaworski, unless otherwise noted.

### <a name="hiera--eyaml_gpg"></a>`hiera::eyaml_gpg`

This calls install and configures hiera-eyaml-gpg

### <a name="hiera--params"></a>`hiera::params`

=== Copyright:

Copyright (C) 2013 Mike Arnold, unless otherwise noted.

## Data types

### <a name="Hiera--Hiera5_defaults"></a>`Hiera::Hiera5_defaults`

This will validate hiera 5 'defaults' hash

Alias of

```puppet
Struct[{
    datadir        => Optional[String],
    data_hash      => Optional[Enum['yaml_data', 'json_data', 'hocon_data']],
    lookup_key     => Optional[String],
    data_dig       => Optional[String],
    hiera3_backend => Optional[String],
    options        => Optional[Hash],
}]
```

### <a name="Hiera--Hiera5_hierarchy"></a>`Hiera::Hiera5_hierarchy`

This will validate hiera 5 hierarchy array hash

Alias of

```puppet
Array[Struct[{
      name            => String,
      path            => Optional[String],
      paths           => Optional[Array[String]],
      glob            => Optional[String],
      globs           => Optional[Array[String]],
      uri             => Optional[String],
      uris            => Optional[Array[String]],
      data_hash       => Optional[String],
      lookup_key      => Optional[String],
      data_dig        => Optional[String],
      datadir         => Optional[String],
      hiera3_backend  => Optional[String],
      options         => Optional[Hash],
}]]
```

