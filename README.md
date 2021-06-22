docker_auth_v2
==============

This role deploys LemonLDAP v2 together with OpenLDAP and PHPLdapAdmin and for SSO authentication

Requirements
------------

None

Role Variables
--------------

Variables from default directory :
* SSO
  * sso_url: URL for SSO
* LDAP
  * ldap_org: Organization name
  * ldap_domain: Organization domain
  * ldap_base_dn: Base Distinguished name (by default "dc=example,dc=org")
  * ldap_admin_pass: Admin user password
  * ldap_config_pass: Configuration user password
  * ldap_readonly_pass: Read-Only user password
  * ldap_url: URL for LDAP
* Backups (for backups to be deployed, host needs to be in maintenance_contract group)
  * swift parameters for 2 object storage instances where backups should be pushed daily
  * auth_backup_pass : Passphrase for encryption of backups


Dependencies
------------

This role requires the following Ansible collection :
* community.docker

This Docker role supposes that Traefik is deployed as an inverseproxy in front of the deployed Dockers.
The following role is used by Le Filament for deploying Traefik : docker_server (https://sources.le-filament.com/lefilament/ansible-roles/docker_server)

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: docker_auth }
      vars:
         - { sso_url: "auth.example.org" }
         - { ldap_url: "ldap.example.org" }
         - { ldap_org: "Example" }
         - { ldap_domain: "example.org" }
         - { ldap_base_dn: "dc=example,dc=org" }
         - { ldap_admin_pass: "AdminPasswordToBeModified" }
         - { ldap_config_pass: "ConfigPasswordToBeModified" }
         - { ldap_readonly_pass: "ReadOnlyPasswordToBeModified" }

License
-------

AGPL-3

Author Information
------------------

Le Filament (https://le-filament.com)
