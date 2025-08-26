# DEPRECATED

This standalone Conjur host identity role is deprecated and no longer maintained.
Please use the version of this role from the [Ansible Conjur Collection](https://github.com/cyberark/ansible-conjur-collection?tab=readme-ov-file#conjur-ansible-role)
instead.

# Conjur Ansible Role

This Ansible role provides the ability to grant Conjur machine identity to a host.
Once a host has an identity created by this role, secrets can be retrieved securely
using the [Summon](https://github.com/cyberark/summon) tool.

## Recommended Reading

* To learn more about Conjur, [give it a try](https://www.conjur.org/get-started/).
* To learn more about how Conjur can be integrated with Ansible, visit the
  [Integration Documentation](https://docs.conjur.org/Latest/en/Content/Integrations/ansible.html).
* To learn more about Summon, the tool that lets you export secret values retrieved
  from Conjur to your applications with, visit the
  [Summon Webpage](https://cyberark.github.io/summon/).
* To learn more about other ways you can integrate with Conjur, visit the
  [Conjur documentation](https://docs.conjur.org/Latest/en/Content/Resources/_TopNav/cc_Home.htm).

## Requirements

* Conjur v1+ or Conjur Enterprise (formerly DAP) v10+
* Conjur Enterprise v4
* Ansible v2.8

If you are using Ansible v2.9+, please consider using our
[Ansible Collection](https://github.com/cyberark/ansible-conjur-collection) instead.

## Using ansible-conjur-host-identity with Conjur Open Source

Are you using this project with [Conjur Open Source](https://github.com/cyberark/conjur)? Then we
**strongly** recommend choosing the version of this project to use from the latest [Conjur OSS
suite release](https://docs.conjur.org/Latest/en/Content/Overview/Conjur-OSS-Suite-Overview.html).
Conjur maintainers perform additional testing on the suite release versions to ensure
compatibility. When possible, upgrade your Conjur version to match the
[latest suite release](https://docs.conjur.org/Latest/en/Content/ReleaseNotes/ConjurOSS-suite-RN.htm);
when using integrations, choose the latest suite release that matches your Conjur version. For any
questions, please contact us on [Discourse](https://discuss.cyberarkcommons.org/c/conjur/5).

## Usage instructions

Install the Conjur role using the following command in your playbook directory:

```sh-session
$ ansible-galaxy install cyberark.conjur-host-identity
```

The Conjur role provides a method to “Conjurize” or establish the Conjur identity
of a remote node with Ansible. The node can then be granted least-privilege access
to retrieve the secrets it needs in a secure manner.

### Role Variables

* `conjur_appliance_url` `*`: The URL of the Conjur / Conjur Enterprise instance you are connecting
   to. When connecting to an HA Conjur Enterprise master cluster, this would be the URL of the
   master load balancer.
* `conjur_account` `*`: The account name for the Conjur instance you are connecting to.
* `conjur_host_factory_token` `*`: [Host Factory](https://docs.conjur.org/Latest/en/Content/Operations/Services/host_factory.html)
  token for layer enrollment. This should be specified in the environment on the
  Ansible controlling host.
* `conjur_host_name` `*`: Name of the host identity for the host factory to create.
* `conjur_ssl_certificate`: The PEM-encoded x509 CA certificate chain for the Conjur Enterprise
  instance you are connecting to. This value may be obtained by running the command:
  ```
  $ openssl s_client -showcerts -servername [CONJUR_DNS_NAME] -connect [CONJUR_DNS_NAME]:443 < /dev/null 2> /dev/null
  ```
* `conjur_validate_certs`: Boolean value to indicate whether the client should
  validate the Conjur server certificates.
* `summon.version`: Version of Summon to install. Default is `0.8.3`.
* `summon_conjur.version`: Version of Summon-Conjur provider to install. Default is `0.5.3`.

The variables marked with `*` are required fields. The other variables are required
for running with an HTTPS Conjur endpoint, but are not required if you run with
an HTTP Conjur endpoint.

### Example Playbook

Configure a remote node with a Conjur identity and Summon:
```yml
- hosts: servers
  roles:
    - role: cyberark.conjur-host-identity
      conjur_appliance_url: 'https://conjur.myorg.com/api',
      conjur_account: 'myorg',
      conjur_host_factory_token: "{{lookup('env', 'HFTOKEN')}}",
      conjur_host_name: "{{inventory_hostname}}"
```

This example:

* Registers the host with Conjur, adding it into the layer specific to the provided
  host factory token.
* Installs Summon with the Summon-Conjur provider for secret retrieval from Conjur.

### Summon & Service Managers
With Summon installed, using Conjur with a Service Manager (like SystemD) becomes a snap.
Here's a simple example of a SystemD file connecting to Conjur:
```ini
[Unit]
Description=DemoApp
After=network-online.target

[Service]
User=DemoUser
#Environment=CONJUR_MAJOR_VERSION=4
ExecStart=/usr/local/bin/summon --yaml 'DB_PASSWORD: !var staging/demoapp/database/password' /usr/local/bin/myapp
```

The example above uses Summon to retrieve the password stored in `staging/myapp/database/password`,
set it to an environment variable `DB_PASSWORD`, and provide it to the demo application
process. Using Summon, the secret is kept off disk. If the service is restarted,
Summon retrieves the password again as the application is started.

### Dependencies

None

### Recommendations

* **Important:** Add `no_log: true` to each play that uses sensitive data,
  **otherwise that data can be printed to the logs.**
* Set the Ansible files to minimum permissions. Ansible uses the permissions of
  the user that runs it.

## Contributing

We welcome contributions of all kinds to this repository. For instructions on
how to get started and descriptions of our development workflows, please see our
[contributing guide][contrib].

[contrib]: https://github.com/cyberark/ansible-conjur-host-identity/blob/master/CONTRIBUTING.md

## License

Copyright (c) 2020 CyberArk Software Ltd. All rights reserved.

This repository is licensed under Apache License 2.0 - see [`LICENSE`](LICENSE)
for more details.
