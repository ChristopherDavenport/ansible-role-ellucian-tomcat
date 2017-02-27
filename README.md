# Ellucian-Tomcat

[![Build Status](https://travis-ci.org/ChristopherDavenport/ansible-role-ellucian-tomcat.svg?branch=master)](https://travis-ci.org/ChristopherDavenport/ansible-role-ellucian-tomcat)

This is a system for installing and managing tomcat configurations for Ellucian.
This fully configures a tomcat instance so that it is ready to deploy according
to Ellucian specifications.

The [full appserver can be found here](https://github.com/ChristopherDavenport/ansible-role-ellucian-appserver-tomcat) which has additional requirements that are not included in this tomcat with specific modifications role.

### Requirements

-   None

## Role Variables

`ellucian_tomcat_db_hostname` is the hostname of your Banner Database  

`ellucian_tomcat_db_port` is the port of the database.  

`ellucian_tomcat_db_sid` is the sid of the database.

`ellucian_tomcat_banproxy_password` and `ellucian_tomcat_banssuser_password`
are required passwords for connecting to the database.

`ellucian_tomcat_extra_libs_path` is a list of extra dependencies to add,
which should be xdb6.jar and ojdbc6.jar

Full list of defaults are

```yaml
# ellucian_tomcat_db_hostname:
# ellucian_tomcat_db_port:
# ellucian_tomcat_db_sid:

# ellucian_tomcat_banproxy_password:
# ellucian_tomcat_banssuser_password:
#
# Optional


# Location Of Extra Libs - ojdbc6.jar and xdb6.jar
# ellucian_tomcat_extra_libs_path:

# Tomcat versions available
# 6.0.47
# 7.0.72
# 8.0.38
# 8.5.6
# 9.0.0.M11
ellucian_tomcat_version: "8.5.6"

ellucian_tomcat_xms: 2048m
ellucian_tomcat_xmx: 4g
ellucian_tomcat_maxpermsize: 1024m

ellucian_tomcat_rim_hostname: "{{ ansible_default_ipv4.address }}"

# One Of SelfService, Admin, Either
ellucian_tomcat_config_type: Either

ellucian_tomcat_timezone: America/NewYork

##### Variables Configured By Initial Variables ###############################

ellucian_tomcat_banproxy_jdbc_url: jdbc:oracle:thin:@//{{ ellucian_tomcat_db_hostname }}:{{ ellucian_tomcat_db_port }}/{{ ellucian_tomcat_db_sid }}
ellucian_tomcat_banproxy_initialsize: "5"
ellucian_tomcat_banproxy_maxactive: "100"
ellucian_tomcat_banproxy_maxidle: "-1"
ellucian_tomcat_banproxy_maxwait: "30000"

ellucian_tomcat_banssuser_jdbc_url: jdbc:oracle:thin:@//{{ ellucian_tomcat_db_hostname }}:{{ ellucian_tomcat_db_port }}/{{ ellucian_tomcat_db_sid }}
ellucian_tomcat_banssuser_initialsize: "5"
ellucian_tomcat_banssuser_maxactive: "100"
ellucian_tomcat_banssuser_maxidle: "-1"
ellucian_tomcat_banssuser_maxwait: "30000"
ellucian_tomcat_logfiledir: "{{ catalina_home }}/logs"

```

## Dependencies

-   [ChristopherDavenport.universal-tomcat](https://galaxy.ansible.com/ChristopherDavenport/universal-tomcat/)
-   [ChristopherDavenport.universal-java](https://galaxy.ansible.com/ChristopherDavenport/universal-java/)

## Example Playbook

```
- hosts: appserver
  vars:
    ellucian_tomcat_db_hostname: banner.test.school.edu
    ellucian_tomcat_db_port: "2322"
    ellucian_tomcat_db_sid: TEST
    ellucian_tomcat_banproxy_password: "fakeBanProxyPass"
    ellucian_tomcat_banssuser_password: "fakeBanSSUserPass"
    ellucian_tomcat_extra_libs_path:
      - "/home/fakeuser/lib/ojdbc6.jar"
      - "/home/fakeuser/lib/xdb6.jar"
  roles:
    - ChristopherDavenport.ellucian-tomcat
```

### License

MIT

### Author Information

This role was created in 2016 by Christopher Davenport.
