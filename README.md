## chensoul-parent

This project houses the parent POM for most ChenSoul projects.

[![Build Status](https://github.com/chensoul/chensoul-parent/actions/workflows/maven-build.yml/badge.svg)](https://github.com/chensoul/chensoul-parent/workflows/maven-build.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent)
[![sonar-quality-gate](https://sonarcloud.io/api/project_badges/measure?project=chensoul-framework&metric=alert_status)](https://sonarcloud.io/dashboard?id=chensoul-framework) 
[![sonar-coverage](https://sonarcloud.io/api/project_badges/measure?project=chensoul-framework&metric=coverage)](https://sonarcloud.io/dashboard?id=chensoul-framework)

### Prerequisites

- Jdk 8+
- Maven 3.2.5

### How to?

```bash
# Clone the repository
$ git clone https://github.com/chensoul/chensoul-parent.git
cd chensoul-parent

./mvnw install -Dgpg.skip=true
```