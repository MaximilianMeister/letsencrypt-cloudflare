letsencrypt-cloudflare
=========

A role to get letsencrypt certificates via dns-01 challenges on cloudflare

Role Variables
--------------

```yml
# CN
lc_common_name: test

# Domain name
lc_domain: my.domain

# Certificate destination path
lc_certificate_destination_path: "{{ '/etc/ssl/' + lc_common_name + '.' + lc_domain + '.crt' }}"

# Certificate Signing Request destination path
lc_csr_destination_path: "{{ '/etc/ssl/' + lc_common_name + '.' + lc_domain + '.csr' }}"

# Certificate Signing Request's private key path
lc_csr_private_key_path: "{{ '/etc/ssl/' + lc_common_name + '.' + lc_domain + '.key' }}"

# Force a challenge
lc_force_challenge: no

# Configure the acme-server endpoint:
#   yes: https://acme-v02.api.letsencrypt.org/directory
#   no: https://acme-staging-v02.api.letsencrypt.org/directory
lc_production: no

# Let's Encrypt account private key
lc_account_private_key: ""

# CLoudflare Email
lc_cloudflare_email: "my@e.mail"

# Cloudflare ApiKey
lc_cloudflare_api_key: "apikey"

# User the certificate should belong to
lc_user: ""

# Group the certificate should belong to
lc_group: ""
```

Dependencies
------------

The below requirements are needed on the host that executes this module.

* `cryptography` python module must be present
* `openSSL` binary must be present

Example Playbook
----------------

```yaml
- hosts: localhost
  become: yes
  roles:
    - letsencrypt-cloudflare
```

Testing
-------

There are a couple of test scenarios that can be run in this role.

**NOTE**: Make sure to set the following variables in the `converge.yml` to sane values in order to successfully run a scenario:

```yaml
- lc_common_name
- lc_domain
- lc_account_private_key
- lc_cloudflare_email
- lc_cloudflare_api_key
```

To run the `default` test that creates a new certificate, execute:

```bash
molecule test
```

To run a specific scenario, execute:

```bash
molecule test --scenario [SCENARIO_NAME]
```

The scenarios can be found under the [molecule](./molecule) folder.

License
-------

MIT
