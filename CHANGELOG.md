# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2020-09-15

### Deprecated
- This repository is deprecated, with all relevant files and tests migrated to the [Ansible Conjur 
  Collection](https://github.com/cyberark/ansible-conjur-collection/).
  [cyberark/conjur-host-identity#30](https://github.com/cyberark/ansible-conjur-host-identity/issues/30)

### Added
- Added daily build trigger

### Changed
- Updated reference to Conjur CLI container
- Updated base image to Ubuntu 18.04
- [Added retries](https://github.com/cyberark/ansible-conjur-host-identity/pull/32) to tasks/identity/Request identity from Conjur.
  This will increase the reliability of host factory requests without introducing any extra delay if the first request succeeds.

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

[Unreleased]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v1.0.0....HEAD
[1.0.0]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.3.1...v1.0.0
[0.3.1]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.3.0...v0.3.1
[0.3.0]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.2.0...v0.3.0
[0.2.0]: https://github.com/cyberark/ansible-conjur-host-identity/compare/v0.1.0...v0.2.0
