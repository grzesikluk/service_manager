### Service manager

#### Description
Simple service manager that should update config and conditionally restart service.

##### How it works
The script defines two roles:
* configuration
* service

`configuration` role is doing update of config files. First it does store old config to `server_config_path`.old file, then
stores new config to `server_config_path`. If old configuration and new configuration differ by MD5 hash - restart
of service will be done by `service` role otherwise restart task will be skipped.

##### Variables
To be able to update variables look into `group_vars/all` to edit file paths and service name.

##### Starting script
You can start the ansible with extra-vars like this:

```bash
ansible-playbook main.yml -i hosts --extra-vars "server_configuration=somecontent"
```

##### Script extra vars

| Name 	| Descripton 	|  Example 	| 
|---	|---	|---	|
|  server_configuration	| Content of configuration that should be stored into config file `server_config_path` 	|  "someparameter=1" 	| 
|  server_config_path	| Path to config file 	|  "/home/user/file.cfg"	| 
|  service 	| Service name to be restarted when config is updated 	| "myservice" 	| 

##### Access rights
Be careful with this script as it uses `root` in hosts definition. As the unix user/group managing the service 
is not known the setup of host should be done appropriately and all user permissions created to ommit the above situation.

##### Extension of this script

It is fairly easy to extend this script adding:
* inventory and hosts files to deploy on other machines and environments
* update of groups_var according to inventory
* adding new roles with their dependencies


Created by lukasz grzesik 2019-09-20