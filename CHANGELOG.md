# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.3.2] - 2020-12-29

### Changed
- Summon and Summon-Conjur default versions are updated to v0.8.3 and v0.5.3,
  respectively.
  [cyberark/ansible-conjur-host-identity#45](https://github.com/cyberark/ansible-conjur-host-identity/issues/45)
- [Added retries](https://github.com/cyberark/ansible-conjur-host-identity/pull/32)
  to tasks/identity/Request identity from Conjur. This will increase the reliability
  of host factory requests without introducing any extra delay if the first request succeeds.

### Removed
- Support for Ansible versions lower than 2.8 is removed in this release since
  these versions are already well past end of life. For Ansible 2.9+, we now
  recommend that users leverage the [Conjur Ansible collection](https://github.com/cyberark/ansible-conjur-collection)
  instead of this project.
  [cyberark/ansible-conjur-host-identity#45](https://github.com/cyberark/ansible-conjur-host-identity/issues/45)

### Deprecated
- Support for Conjur Enterprise v4 is deprecated in this release. It will be removed
  in the next release.
  [cyberark/ansible-conjur-host-identity#45](https://github.com/cyberark/ansible-conjur-host-identity/issues/45)

## [0.3.1] - 2019-02-27
### Fixed
- Fix final ansible-lint warnings that are fixable

## [0.3.0] - 2019-02-26
### Fixed
- Fixed Ansible Galaxy import warnings

## [0.2.0] - 2019-02-26
### Added
- Added platform support for RHEL/CentOS 7

## 0.1.0 - 2018-03-08
### Added
- Initial release
- Establishes Conjur identity using a Conjur Host Factory Token
- Installs and configures Summon Summon-Conjur provider for secure secret retrieval

[Unreleased]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.3.2...HEAD
[0.3.2]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.3.1...v0.3.2
[0.3.1]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.3.0...v0.3.1
[0.3.0]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.1.0...v0.2.0
