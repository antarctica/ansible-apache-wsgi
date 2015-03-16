# Apache WSGI (`apache-wsgi`)

**Part of the BAS Ansible Role Collection (BARC)**

Configures Apache to support WSGI compatible applications through the WSGI Apache module

## Overview

* Restarts Apache to pick up WSGI module
* Creates an includes file containing module configuration and loads this within the default virtual host

## Availability

This role is designed for internal use but if useful can be shared publicly.

## Usage

### Requirements

#### BAS Ansible Role Collection (BARC)

* `apache`

### Variables

* `apache_wsgi_config_file_path`
    * Path consisting of directory and file name for the file that will contain this module's configuration options
    * This variable **MUST** be a valid UNIX path and **SHOULD NOT** exist.
    * Default: "/etc/apache2/conf-available/mod-wsgi.conf"
* `apache_wsgi_option_script_alias_directory`
    * A directory that will contain WSGI scripts, used by the script_alias directive to forward requests to WSGI scripts
    * This variable **MUST** be a valid UNIX path without a trailing slash (i.e. `/`).
    * If a non-default root is used you **MUST** ensure the `www-data` group has access.
    * By default it is assumed a "wsgi-scripts" directory will exist in the document root.
    * Default: "{{ apache_default_var_www_document_root }}/wsgi-scripts"
* apache_wsgi_option_script_alias`
    * Maps a URL to a filesystem location and designates the target as a WSGI script
    * For more information see the [module's documentation for this directive](https://code.google.com/p/modwsgi/wiki/ConfigurationDirectives#WSGIScriptAlias).
    * By default all requests are forwarded to the wsgi_scripts directory set by `apache_wsgi_option_script_alias_directory`.
    * Default: "/ {{ apache_wsgi_option_script_alias_directory }}"

* `apache_wsgi_option_pass_authorization`
    * Enable/Disable passing of authorisation headers
    * For more information see the [module's documentation for this directive](https://code.google.com/p/modwsgi/wiki/ConfigurationDirectives#WSGIPassAuthorization).
    * You **MUST** quote this value or Ansible will evaluate this value to a "True" or "False" which are not valid.
    * Allowed values: "on" or "off".
    * Default: "On"

## Contributing

This project welcomes contributions, see `CONTRIBUTING` for our general policy.

## Developing

### Committing changes

The [Git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) workflow is used to manage development of this package.

Discrete changes should be made within *feature* branches, created from and merged back into *develop* (where small one-line changes may be made directly).

When ready to release a set of features/changes create a *release* branch from *develop*, update documentation as required and merge into *master* with a tagged, [semantic version](http://semver.org/) (e.g. `v1.2.3`).

After releases the *master* branch should be merged with *develop* to restart the process. High impact bugs can be addressed in *hotfix* branches, created from and merged into *master* directly (and then into *develop*).

### Issue tracking

Issues, bugs, improvements, questions, suggestions and other tasks related to this package are managed through the BAS Web & Applications Team Jira project ([BASWEB](https://jira.ceh.ac.uk/browse/BASWEB)).

## License

Copyright 2015 NERC BAS. Licensed under the MIT license, see `LICENSE` for details.