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
    <version>1.0.40</version>
    <relativePath/>
</parent>
```

## GPG

After generating gpg key following by [here](https://central.sonatype.org/publish/requirements/gpg/#generating-a-key-pair)

```bash
gpg --full-generate-key
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

Distribute your public key:

```bash
gpg --keyserver hkp://keyserver.ubuntu.com:11371 --send-keys <YOUR_KEY>

gpg --keyserver hkp://keyserver.ubuntu.com:11371 --recv-keys <YOUR_KEY>
```

Or upload your public key by https://keys.openpgp.org/upload.

```bash
gpg --export xxx@xxx.com > my_key.pub
```

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

In order to perform a release deployment you have to edit your version in all your POM files to use release versions.

```bash
mvn versions:set -DnewVersion=1.2.3 versions:commit
```

Install to local repository `~/.m2/repository`:

```bash
mvn clean install
```

Release to the staging repository with the release profile:

```bash
mvn clean deploy -P release -Dgpg.passphrase=yourpassphrase
```

And then login to the staging repository https://s01.oss.sonatype.org/#stagingRepositories , release and drop the repository.
Wait a few minutes and then you can find the release version in https://central.sonatype.com/artifact/com.chensoul/chensoul-parent/
or https://s01.oss.sonatype.org/service/local/repositories/releases/content/com/chensoul/chensoul-parent/ .

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
