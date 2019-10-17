# ansible-role-solr-core-config

Copy a config set from an arbitrary location (ie one that ships with the solr drupal module) into the solr core's config directory.

This is meant to be used in conjunction with (and after both of) GeerlingGuy's solr role, and Acro Media's virtual host role.

**Warning**: All of the contents of  `/{{ solr_home }}/data/{{ solr_core_name }}/conf` will be replaced by the contents of `{{ solr_core_conf_source }}`. If you want your conf dir backed up, you'll need to do that before running this role.


## Requirements

* Your solr core's conf directory must already exist
* Your source core conf files must already exist on the server


## Role Variables

### Required:
* **solr_core_conf_source**: Absolute path to the directory on the server that contains your config set
* **solr_core_name**: Name of the solr core installed in

### Optional:
* **solr_service_name**: In case your solr service is named something other than `solr`.
* **solr_home**: In case your solr files were configured somewhere other than `/var/solr`


## Dependencies

None


## Example Playbooks

```yaml
    - hosts: servers
      roles:
        - name: Configure solr core XYZ in the default solr installation
          role: acromedia.solr-core-config
          vars:
            solr_core_conf_source: /var/www/html/siteXYZ/modules/contrib/search_api_solr/solr-conf/6.x
            solr_core_name: coreXYZ
```

```yaml
    - hosts: servers
      roles:
        - name: Configure a 2nd solr core running for a different version of solr (7), which is side by side with the first (6)
          role: acromedia.solr-core-config
          vars:
            solr_core_conf_source: /var/www/html/siteABC/modules/contrib/search_api_solr/solr-conf/7.x
            solr_core_name: coreABC
            solr_service_name: solr7
            solr_home: /var/solr7
```


## License

GPLv3


## Author Information

Acro Media Inc.
