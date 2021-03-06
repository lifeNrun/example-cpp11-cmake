# [Codecov][1] CI CMake g++ cpp11 lcov Example
[![Travis CI logo][travis-image]][travis-link]
[![Codecov logo][codecov-image]][codecov-link]

[![Build Status][travis-badge]][travis-link]
[![codecov][codecov-badge]][codecov-link]
[![MIT License][license-badge]](LICENSE.md)

The goal of this project is to build project with following tools:
 * C++ version: `C++11`
 * Build system: [`CMake`](https://cmake.org/)
 * C++ compiler: `g++`
 * Libraries: `STL` only
 * Code coverage: [`lcov`](http://ltp.sourceforge.net/coverage/lcov.php) (note: it should show the code coverage is below 100%)
 * [`CodeCov`](https://codecov.io/) (code coverage is measured by CodeCov).
 * Source: multiple files

## Special Thanks
Goes to [Richel Bilderbeek](https://github.com/richelbilderbeek) for inspiration and all work on [Travis CI tutorials](https://github.com/richelbilderbeek/travis_cpp_tutorial). 
Here is [link](https://github.com/richelbilderbeek/travis_cmake_gcc_cpp11) to the same project with structure (except no `lcov`) and here is [list](https://github.com/richelbilderbeek/travis_cpp_tutorial/blob/master/statuses.md) of all his projects if you want make build with travis but with different configuration.

## Prerequisites

To build the project you need to install `CMake`. [Here](https://cmake.org/install/) are the instructions. To create code coverage report you need to install `lcov`. [`Download lcov`](http://ltp.sourceforge.net/coverage/lcov.php) from here you can download latest `lcov` and here are [`instructions`](http://ltp.sourceforge.net/coverage/lcov/readme.php). This reports will be later uploaded to CodeCov servers.

## Guide
### Travis Setup

Add to your `.travis.yml` file.
```yml
language: cpp
compiler:
- g++
after_success:
    # Creating report
  - cd ${TRAVIS_BUILD_DIR}
  - lcov --directory . --capture --output-file coverage.info # capture coverage info
  - lcov --remove coverage.info '/usr/*' --output-file coverage.info # filter out system
  - lcov --list coverage.info #debug info
  # Uploading report to CodeCov
  - bash <(curl -s https://codecov.io/bash) || echo "Codecov did not collect coverage reports"
```
### Produce Coverage Reports
#### lcov
Gather reports:
```sh
lcov --directory . --capture --output-file coverage.info
```
## Caveats
### Private Repos
Add to your `.travis.yml` file.
```yml
after_success:
  - bash <(curl -s https://codecov.io/bash) -t uuid-repo-token
```

## Support
### Contact
- Intercom (in-app messanger)
- Email: [support@codecov.io](mailto:support@codecov.io)
- Slack: [slack.codecov.io](https://slack.codecov.io)
- [gh/codecov/support](https://github.com/codecov/support)


## Authors
* **RokKos** - [RokKos](https://github.com/RokKos)
* **Rolf Eike Beer** - [DerDakon](https://github.com/DerDakon)

## License
This project is licensed under the MIT License - see the [LICENSE](https://github.com/RokKos/classes-c-/blob/master/LICENSE) file for details.

1. More documentation at https://docs.codecov.io
2. Configure codecov through the `codecov.yml`  https://docs.codecov.io/docs/codecov-yaml

[1]: https://codecov.io/
[travis-badge]:    https://travis-ci.org/codecov/example-cpp11-cmake.svg?branch=master
[travis-link]:     https://travis-ci.org/codecov/example-cpp11-cmake
[travis-image]:    https://github.com/codecov/example-cpp1-cmake/blob/master/img/TravisCI.png
[license-badge]:   https://img.shields.io/badge/license-MIT-007EC7.svg
[codecov-badge]:   https://codecov.io/gh/codecov/example-cpp11-cmake/branch/master/graph/badge.svg
[codecov-link]:    https://codecov.io/gh/codecov/example-cpp11-cmake
[codecov-image]:   https://github.com/codecov/example-cpp1-cmake/blob/master/img/Codecov.png
