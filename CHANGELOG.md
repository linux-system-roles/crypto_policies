Changelog
=========

[1.4.0] - 2024-08-01
--------------------

### New Features

- Handle reboot for transactional update systems (#121)

### Other Changes

- ci: Add tft plan and workflow (#120)
- ci: Update fmf plan to add a separate job to prepare managed nodes (#122)
- ci: Bump sclorg/testing-farm-as-github-action from 2 to 3 (#123)

[1.3.5] - 2024-07-02
--------------------

### Bug Fixes

- fix: add support for EL10 (#118)

### Other Changes

- ci: ansible-lint action now requires absolute directory (#117)

[1.3.4] - 2024-06-11
--------------------

### Other Changes

- ci: use tox-lsr 3.3.0 which uses ansible-test 2.17 (#112)
- ci: tox-lsr 3.4.0 - fix py27 tests; move other checks to py310 (#114)
- ci: Add supported_ansible_also to .ansible-lint (#115)

[1.3.3] - 2024-04-04
--------------------

### Other Changes

- ci: fix python unit test - copy pytest config to tests/unit (#108)
- ci: Bump ansible/ansible-lint from 6 to 24 (#109)
- ci: Bump mathieudutour/github-tag-action from 6.1 to 6.2 (#110)

[1.3.2] - 2024-01-16
--------------------

### Other Changes

- ci: Use supported ansible-lint action; run ansible-lint against the collection (#105)

[1.3.2] - 2024-01-16
--------------------

### Other Changes

- ci: Use supported ansible-lint action; run ansible-lint against the collection (#105)
- ci: Use supported ansible-lint action; run ansible-lint against the collection (#106)

[1.3.1] - 2023-12-08
--------------------

### Other Changes

- ci: bump actions/github-script from 6 to 7 (#102)
- refactor: get_ostree_data.sh use env shebang - remove from .sanity* (#103)

[1.3.0] - 2023-11-29
--------------------

### New Features

- feat: support for ostree systems (#99)

### Other Changes

- Bump actions/checkout from 3 to 4 (#90)
- ci: ensure dependabot git commit message conforms to commitlint (#93)
- ci: tox-lsr version 3.1.1 (#97)

[1.2.12] - 2023-09-08
--------------------

### Other Changes

- ci: Add markdownlint, test_converting_readme, and build_docs workflows (#86)

  - markdownlint runs against README.md to avoid any issues with
    converting it to HTML
  - test_converting_readme converts README.md > HTML and uploads this test
    artifact to ensure that conversion works fine
  - build_docs converts README.md > HTML and pushes the result to the
    docs branch to publish dosc to GitHub pages site.
  - Fix markdown issues in README.md
  
  Signed-off-by: Sergei Petrosian <spetrosi@redhat.com>

- docs: Make badges consistent, run markdownlint on all .md files (#87)

  - Consistently generate badges for GH workflows in README RHELPLAN-146921
  - Run markdownlint on all .md files
  - Add custom-woke-action if not used already
  - Rename woke action to Woke for a pretty badge
  
  Signed-off-by: Sergei Petrosian <spetrosi@redhat.com>

- ci: Remove badges from README.md prior to converting to HTML (#88)

  - Remove thematic break after badges
  - Remove badges from README.md prior to converting to HTML
  
  Signed-off-by: Sergei Petrosian <spetrosi@redhat.com>

[1.2.11] - 2023-07-19
--------------------

### Bug Fixes

- fix: facts being gathered unnecessarily (#84)

### Other Changes

- ci: Add pull request template and run commitlint on PR title only (#81)
- ci: Rename commitlint to PR title Lint, echo PR titles from env var (#82)
- ci: ansible-lint - ignore var-naming[no-role-prefix] (#83)

[1.2.10] - 2023-05-26
--------------------

### Other Changes

- docs: Consistent contributing.md for all roles - allow role specific contributing.md section
- docs: remove unused Dependencies section in README

[1.2.9] - 2023-04-13
--------------------

### Other Changes

- ansible-lint - add changed_when true (#70)

[1.2.8] - 2023-04-06
--------------------

### Other Changes

- Add README-ansible.md to refer Ansible intro page on linux-system-roles.github.io (#68)

[1.2.7] - 2023-01-20
--------------------

### New Features

- none

### Bug Fixes

- ansible-lint 6.x fixes (#55)

### Other Changes

- Add check for non-inclusive language
- cleanup non-inclusive words.

[1.2.6] - 2022-07-19
--------------------

### New Features

- none

### Bug Fixes

- none

### Other Changes

- Ensure role tests work with gather_facts: false (#41)

Ensure role tests work when using ANSIBLE_GATHERING=explicit

- Add cleanup to some tests to facilitate 'shared' test runs (#42)

crypto_policies_reboot_required being a tri-state
doesn't allow me to do that cleanly

- make min_ansible_version a string in meta/main.yml (#43)

The Ansible developers say that `min_ansible_version` in meta/main.yml
must be a `string` value like `"2.9"`, not a `float` value like `2.9`.

- Add CHANGELOG.md (#44)

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
- update to tox-lsr 2.4.0 - add support for ansible-test with docker

- tests: Use a module that is available in all systems
- Emptying the skip list of .ansible-lint.
- CI: Add support for RHEL-9
- use tox-lsr 2.3.0 and enable ansible-test
- Fix ansible-test errors

[1.0.0] - 2021-02-11
--------------------

### Initial Release
