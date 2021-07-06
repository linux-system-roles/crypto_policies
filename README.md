# crypto_policies
![CI Testing](https://github.com/linux-system-roles/crypto_policies/workflows/tox/badge.svg)


This Ansible role manages system-wide crypto policies.

This concept is well adopted since Red Hat Enterprise Linux 8 and in Fedora.

## Requirements

The system-wide crypto policies are implemented and tested on RHEL 8/CentOS 8
and Fedora.

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

## Dependencies

None.

## Example Playbook

The following playbook configures the system to the default crypto policy
level without SHA1. The update is done without reboot (which is recommended
to do by the user afterwards).

```yaml
- hosts: all
  roles:
    role: linux-system-roles.crypto_policies
    vars:
      crypto_policies_policy: "DEFAULT:NO-SHA1"
      crypto_policies_reload: false

```

## License

MIT, see the file LICENSE for more information.

## Author Information

Jakub Jelen, 2020
