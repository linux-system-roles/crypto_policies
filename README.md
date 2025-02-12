# crypto_policies

[![ansible-lint.yml](https://github.com/linux-system-roles/crypto_policies/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/linux-system-roles/crypto_policies/actions/workflows/ansible-lint.yml) [![ansible-test.yml](https://github.com/linux-system-roles/crypto_policies/actions/workflows/ansible-test.yml/badge.svg)](https://github.com/linux-system-roles/crypto_policies/actions/workflows/ansible-test.yml) [![codespell.yml](https://github.com/linux-system-roles/crypto_policies/actions/workflows/codespell.yml/badge.svg)](https://github.com/linux-system-roles/crypto_policies/actions/workflows/codespell.yml) [![markdownlint.yml](https://github.com/linux-system-roles/crypto_policies/actions/workflows/markdownlint.yml/badge.svg)](https://github.com/linux-system-roles/crypto_policies/actions/workflows/markdownlint.yml) [![tft.yml](https://github.com/linux-system-roles/crypto_policies/actions/workflows/tft.yml/badge.svg)](https://github.com/linux-system-roles/crypto_policies/actions/workflows/tft.yml) [![tft_citest_bad.yml](https://github.com/linux-system-roles/crypto_policies/actions/workflows/tft_citest_bad.yml/badge.svg)](https://github.com/linux-system-roles/crypto_policies/actions/workflows/tft_citest_bad.yml) [![woke.yml](https://github.com/linux-system-roles/crypto_policies/actions/workflows/woke.yml/badge.svg)](https://github.com/linux-system-roles/crypto_policies/actions/workflows/woke.yml)

This Ansible role manages system-wide crypto policies.

This concept is well adopted since Red Hat Enterprise Linux 8 and in Fedora.

## Requirements

See below

### Collection requirements

If you want to manage `rpm-ostree` systems with this role, you will need to
install additional collections.  Please run the following command line to
install the collection.

```bash
ansible-galaxy collection install -vv -r meta/collection-requirements.yml
```

## Role Variables

By default, this role will just report system status as described in the
following section.

* `crypto_policies_policy`

Use this variable to specify the desired crypto policy on the target system,
which can be either the base policy or a base policy with subpolicies
as accepted by the `update-crypto-policies` tool. For example `FUTURE` or
`DEFAULT:NO-SHA1:GOST`. The specified base policy and subpolicies
must be available on the target system.

The default value is `null` meaning the configuration is not changed and
the role will just collect the facts below.

The list of available base policies on the target system can be found in the
`crypto_policies_available_policies` variable and the list of available
subpolicies can be found in the `crypto_policies_available_subpolicies` variable.

* `crypto_policies_reload`

By default (`true`), updating crypto policies forces reload of some of
the daemons affected by crypto policies in the system. Setting `false`
prevents this behavior and is helpful if the role is executed during system
enrollment or some other follow-up tasks is expected to do it later.

* `crypto_policies_reboot_ok`

Crypto policies can not know all the custom applications using crypto
libraries that are affected by change of crypto policies so it is recommended
to reboot after changing crypto policies to make sure all of the services
and applications will read the new configuration files. By default (`false`),
if reboot is required, this role will set `crypto_policies_reboot_required`
variable as described below and it is up to the user of the role to reboot
the system afterwards, for example after applying some other changes that might
need reboot. If there are no other tasks in the playbook that require reboot,
you can set this value to `true` and this role will handle the reboot for you,
when needed.

* `crypto_policies_transactional_update_reboot_ok`

This variable is used to handle reboots required by transactional updates.
If a transactional update requires a reboot, the role will proceed with the
reboot if `crypto_policies_transactional_update_reboot_ok` is set to `true`. If set
to `false`, the role will notify the user that a reboot is required, allowing
for custom handling of the reboot requirement. If this variable is not set,
the role will fail to ensure the reboot requirement is not overlooked.

### Variables Exported by the Role

* `crypto_policies_active`

This fact contains the currently active policy name in the format as accepted
by `crypto_policies_policy` variable above.

* `crypto_policies_available_policies`

This is a list of all base policies available on the target system.
Custom policy files can be installed by copying the `.pol` files into
`/etc/crypto-policies/policies` directory (not implemented in this role yet).

* `crypto_policies_available_subpolicies`

This is a list of all subpolicies available on the target system.
Custom subpolicies can be installed by copying the `.pmod` files into
`/etc/crypto-policies/policies/modules` directory (not implemented in this
role yet).

* `crypto_policies_available_modules`

Deprecated alias to `crypto_policies_available_subpolicies`.

* `crypto_policies_reboot_required`

Default `false` - if `true`, this means a reboot is needed to apply
the changes made by the role

## Example Playbook

The following playbook configures the system to the default crypto policy
level without SHA1. The update is done without reboot (which is recommended
to do by the user afterwards).

```yaml
- name: Manage crypto policies
  hosts: all
  roles:
    - role: linux-system-roles.crypto_policies
      vars:
        crypto_policies_policy: "DEFAULT:NO-SHA1"
        crypto_policies_reload: false

```

## rpm-ostree

See README-ostree.md

## License

MIT, see the file LICENSE for more information.

## Author Information

Jakub Jelen, 2020
