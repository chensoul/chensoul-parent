# ChenSoul™: Parent POM

<p align="center">
  <a href="https://search.maven.org/artifact/com.chensoul/chensoul-parent">
    <img alt="maven" src="https://img.shields.io/maven-central/v/com.chensoul/chensoul-parent.svg?style=flat-square"/>
  </a>

  <a href="https://www.apache.org/licenses/LICENSE-2.0">
    <img alt="code style" src="https://img.shields.io/badge/license-Apache%202-4EB1BA.svg?style=flat-square"/>
  </a>
</p>

This project houses the parent Project Object Model (POM) for most ChenSoul™ projects.

## Status

This project is currently experimental, in a pre-alpha state, and unsuitable for production use.

## Compatibility

**Until further notice, this project's APIs are subject to frequent backwards-incompatible signature and behavior
changes, regardless of project version and without notice.**

## Requirements

ChenSoul™ Parent POM requires a Java runtime of version 1.8 or higher.

## Installation

ChenSoul™ Parent POM is, or will be, available on [Maven Central](https://search.maven.org/artifact/com.chensoul/chensoul-parent). Using ChenSoul™ Parent POM as a Maven pom:

```xml

<parent>
    <groupId>com.chensoul</groupId>
    <artifactId>chensoul-parent</artifactId>
    <!-- Always check https://search.maven.org/artifact/com.chensoul/chensoul-parent for up-to-date available versions. -->
    <version>1.1.0</version>
    <relativePath/>
</parent>
```

## GPG

After generating gpg key following
by [here](https://central.sonatype.org/publish/requirements/gpg/#generating-a-key-pair)

```bash
gpg --gen-key
```

You can list the local key that you created:

```bash
gpg --list-secret-keys --keyid-format=long
```

Then you can export the private key to your local machine in order to upload it later to Github secret:

```bash
gpg --armor --export-secret-keys <YOUR_KEY> > private.gpg
```

* YOUR_KEY='long number'

## Usage

Check your maven settings file `～/.m2/settings.xml`:

```bash
    <server>
        <id>gpg.passphrase</id>
        <passphrase><PASSPHRASE_GPG></passphrase>
    </server>
    <server>
        <id>ossrh</id>
        <username><OSSRH_USERNAME></username>
        <password><OSSRH_TOKEN></password>
    </server>
```

According to [publish-maven](https://central.sonatype.org/publish/publish-maven/), you can do these as below.

### Performing a Snapshot Deployment

Snapshot deployment are performed when your version ends in -SNAPSHOT . You do not need to fulfill the requirements when
performing snapshot deployments and can simply run

```bash
mvn -B clean deploy
```

SNAPSHOT versions are not synchronized to the Central Repository. If you wish your users to consume your SNAPSHOT
versions, they would need to add the snapshot repository to their Nexus Repository Manager, settings.xml, or pom.xml.
Successfully deployed SNAPSHOT versions will be found in https://s01.oss.sonatype.org/content/repositories/snapshots/

### Performing a Release Deployment

Change version with the Maven versions plugin.

```bash
mvn versions:set -DnewVersion=1.2.3 versions:commit
```

Release to the staging repository https://s01.oss.sonatype.org/service/local/staging/deploy/maven2/ with the release profile:

```bash
mvn clean deploy -P release
```

Release to the central repository:

```bash
mvn clean deploy -P release -DautoReleaseAfterClose=true
```

### Manually Releasing the Deployment to the Central Repository

You can simply release the staging repository with

```bash
mvn clean nexus-staging:release -P release -DautoReleaseAfterClose=true
```

### Manually Publish the site to github pages

Publish to github pages:

```bash
mvn clean site scm-publish:publish-scm
```

## Links

Login to your [sonatype](https://s01.oss.sonatype.org/) account to release the version

| Type     | URL                                                                                                   | Description                |
|:---------|:------------------------------------------------------------------------------------------------------|:---------------------------|
| Snapshot | [sonatype](https://s01.oss.sonatype.org/content/repositories/snapshots/com/chensoul/chensoul-parent/) | Sonatype Snapshot versions |
| Release  | [maven](https://repo.maven.apache.org/maven2/com/chensoul/chensoul-parent/)                           | Maven Release versions     |
| Release  | [central-sonatype](https://central.sonatype.com/artifact/com.chensoul/chensoul-parent/)               | Sonatype Release versions  |

## Documentation

Full documentation is, or will be, available
at [chensoul.github.io/chensoul-parent](https://chensoul.github.io/chensoul-parent/).
