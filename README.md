# ansible-role-solr-core-config

![.github/workflows/molecule.yml](https://github.com/AcroMedia/ansible-role-solr-core-config/workflows/.github/workflows/molecule.yml/badge.svg)

Copy a config set from an arbitrary location (ie one that ships with the solr drupal module) into the solr core's config directory.

This is meant to be used in conjunction with (and after both of) GeerlingGuy's solr role, and Acro Media's virtual host role.

**Warning**: All of the contents of  `/{{ solr_home }}/data/{{ solr_core_name }}/conf` will be replaced by the contents of `{{ solr_core_conf_source }}`. If you want your conf dir backed up, you'll need to do that before running this role.


## Requirements

* Your `solr_core_conf_dest` directory must already exist. I.e. You must have already created the solr core. If you're using [GeerlingGuy's solr role](https://github.com/geerlingguy/ansible-role-solr), then list your core name as one of the items in the `solr_cores` variable. Or create your core manually in the Solr UI. Or run the solr cli to create your core.
* Your source core conf files must already exist on the server. E.g. Export your solr core config from your Drupal 8 site, commit that extracted folder to a folder outside your web root, and deploy the code to your server.


## Role Variables

### Required:
* **solr_core_conf_source**: Absolute path to the directory on the server that contains your config set
* **solr_core_name**: Name of the solr core installed in

### Optional:
* **solr_service_name**: In case your solr service is named something other than `solr`.
* **solr_home**: In case your solr files were configured somewhere other than `/var/solr`
* **solr_core_conf_dest**: Defaults to `"{{ solr_home }}/data/{{ solr_core_name }}/conf"`. You shouldn't ever need to change this. It's only noted here, because it's very easy to miss creating your core before using t his role. This role does not create the solr core for you.

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
