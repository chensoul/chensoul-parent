# chensoul-parent

[![Build Status](https://github.com/chensoul/chensoul-parent/actions/workflows/maven-build.yml/badge.svg)](https://github.com/chensoul/chensoul-parent/workflows/maven-build.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Maven Central][maven-image]][maven-url]

ChenSoul Parent BOM

## Prerequisites

- Jdk 8+
- Maven 3.2.5

## How to?

```bash
# Clone the repository
$ git clone https://github.com/chensoul/chensoul-parent.git
cd chensoul-parent

./mvnw install -Dgpg.skip=true
```

## Sonar Analysis Result

[![sonar-quality-gate][sonar-quality-gate]][sonar-url] [![sonar-coverage][sonar-coverage]][sonar-url] [![sonar-bugs][sonar-bugs]][sonar-url] [![sonar-vulnerabilities][sonar-vulnerabilities]][sonar-url]

## References

- [https://github.com/jhipster/jhipster-bom](https://github.com/jhipster/jhipster-bom)


[maven-image]: https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent/badge.svg
[maven-url]: https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent

[sonar-url]: https://sonarcloud.io/dashboard?id=chensoul-framework
[sonar-quality-gate]: https://sonarcloud.io/api/project_badges/measure?project=chensoul-framework&metric=alert_status
[sonar-coverage]: https://sonarcloud.io/api/project_badges/measure?project=chensoul-framework&metric=coverage
[sonar-bugs]: https://sonarcloud.io/api/project_badges/measure?project=chensoul-framework&metric=bugs
[sonar-vulnerabilities]: https://sonarcloud.io/api/project_badges/measure?project=chensoul-framework&metric=vulnerabilities