# ChenSoul™: Parent POM

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent)

This project houses the parent Project Object Model (POM) for most ChenSoul™ projects.

# Status

This project is currently experimental, in a pre-alpha state, and unsuitable for production use.

# Compatibility

**Until further notice, this project's APIs are subject to frequent backwards-incompatible signature and behavior changes, regardless of project version and without notice.**

# Requirements

ChenSoul™ Parent POM requires a Java runtime of version 1.8 or higher.

# Installation

ChenSoul™ Parent POM is, or will be, available on [Maven Central](https://search.maven.org/artifact/com.chensoul/chensoul-parent).  Using ChenSoul™ Parent POM as a Maven pom:

```xml
<parent>
    <groupId>com.chensoul</groupId>
    <artifactId>chensoul-parent</artifactId>
    <!-- Always check https://search.maven.org/artifact/com.chensoul/chensoul-parent for up-to-date available versions. -->
    <version>1.0.10</version>
    <relativePath/>
</parent>
```

# Usage

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

Update pom version:

```bash
mvn -B build-helper:parse-version versions:set -DnewVersion=0.0.2-SNAPSHOT versions:commit 
```

Create new branch with next version, it won't update the working copy version:

```bash
mvn -B release:branch -DbranchName=my-branch -DupdateBranchVersions=true -DupdateWorkingCopyVersions=false
```

Release to local staging (push tag to github using username and password):

```bash
mvn -B release:clean release:prepare release:perform
```

GPG to sign and release to sonatype using release profile:

```bash
mvn -B clean deploy -Prelease -Dgpg.passphrase=<PASSPHRASE_GPG> -Dusername=<OSSRH_USERNAME> -Dpassword=<OSSRH_TOKEN>

# reading gpg.passphrase, username and password from settings.xml
mvn -B clean deploy -Prelease
```

Release to sonatype (push tag to github using username and password); sign and snapshot to local staging:

```bash
mvn -B release:clean release:prepare release:perform deploy -Prelease -DautoReleaseAfterClose=true
```

# Documentation

Full documentation is, or will be, available at [chensoul.github.io/chensoul-parent](https://chensoul.github.io/chensoul-parent/).
