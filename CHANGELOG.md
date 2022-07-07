Changelog
=========

[1.2.5] - 2022-05-06
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- bump tox-lsr version to 2.11.0; remove py37; add py310
- Add tests::reboot tag

[1.2.4] - 2022-04-12
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- support gather\_facts: false; support setup-snapshot.yml
- bump tox-lsr version to 2.10.1

[1.2.3] - 2022-01-10
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- bump tox-lsr version to 2.8.3
- change recursive role symlink to individual role dir symlinks
- Run the new tox test

[1.2.2] - 2021-11-08
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- update tox-lsr version to 2.7.1
- support python 39, ansible-core 2.12, ansible-plugin-scan

[1.2.1] - 2021-09-13
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- use apt-get install -y
- use tox-lsr version 2.5.1

[1.2.0] - 2021-08-10
--------------------

### New features

- Drop support for Ansible 2.8 by bumping the Ansible version to 2.9

### Bug Fixes

- none

### Other Changes

- none

[1.1.0] - 2021-07-06
--------------------

### New features

- rename 'policy modules' to 'subpolicies'

### Bug Fixes

- none

### Other Changes

- none

[1.0.1] - 2021-04-07
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- Remove python-26 environment from tox testing
- update to tox-lsr 2.4.0 - add support for ansible-test sanity with docker
- tests: Use a module that is available in all systems
- Emptying the skip list of .ansible-lint.
- CI: Add support for RHEL-9
- use tox-lsr 2.3.0 and enable ansible-test
- Fix ansible-test errors

[1.0.0] - 2021-02-11
--------------------

### Initial Release
