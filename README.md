# Ellucian-Tomcat

[![Build Status](https://travis-ci.org/ChristopherDavenport/ansible-role-ellucian-tomcat.svg?branch=master)](https://travis-ci.org/ChristopherDavenport/ansible-role-ellucian-tomcat)

This is a system for installing and managing tomcat configurations for Ellucian.
This fully configures a tomcat instance so that it is ready to deploy according
to Ellucian specifications.

### Requirements

Some Version Of Java with `JAVA_HOME` being populated.
Requires `java_home` ansible variable to be populated to configure service.
