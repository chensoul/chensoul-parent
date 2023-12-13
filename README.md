# ChenSoul™: Parent POM

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent)

This project houses the parent Project Object Model (POM) for most ChenSoul™ projects.

## Status

This project is currently experimental, in a pre-alpha state, and unsuitable for production use.

## Compatibility

**Until further notice, this project's APIs are subject to frequent backwards-incompatible signature and behavior changes, regardless of project version and without notice.**

## Requirements

ChenSoul™ Parent POM requires a Java runtime of version 1.8 or higher.

## Installation

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

## GPG

After generating gpg key following by [here](https://central.sonatype.org/publish/requirements/gpg/#generating-a-key-pair)

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

Snapshot deployment are performed when your version ends in -SNAPSHOT . You do not need to fulfill the requirements when performing snapshot deployments and can simply run

```bash
mvn -B clean deploy
```

SNAPSHOT versions are not synchronized to the Central Repository. If you wish your users to consume your SNAPSHOT versions, they would need to add the snapshot repository to their Nexus Repository Manager, settings.xml, or pom.xml. Successfully deployed SNAPSHOT versions will be found in https://s01.oss.sonatype.org/content/repositories/snapshots/


### Performing a Release Deployment

The change of the versions for your project, and the parent references in a multi module setup, can be performed manually or with the help of the Maven versions plugin.

```bash
mvn versions:set -DnewVersion=1.2.3 versions:commit
```

Once you have updated all the versions and ensured that your build passes without deployment you can perform the deployment with the usage of the release profile with

```bash
mvn clean deploy -P release
```

By default, the deployment will be performed to the staging repository https://s01.oss.sonatype.org/service/local/staging/deploy/maven2/ . You can release the deployment to the central repository:

```bash
mvn clean deploy -P release -DautoReleaseAfterClose=true
```

### Performing a Release Deployment with the Maven Release Plugin

The configuration for the Maven release plugin should include disabling the release profile that is part of the Maven Super POM, since we are using our own profile, and specify the deploy goal together with the activation of our release profile

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-release-plugin</artifactId>
  <version>2.5.3</version>
  <configuration>
    <autoVersionSubmodules>true</autoVersionSubmodules>
    <useReleaseProfile>false</useReleaseProfile>
    <releaseProfiles>release</releaseProfiles>
    <goals>deploy</goals>
  </configuration>
</plugin>
```

With the SCM connection configured correctly you can perform a release deployment to OSSRH with

```bash
mvn -B -X release:clean release:prepare release:perform -DreleaseVersion= -DdevelopmentVersion= -DautoReleaseAfterClose=true
```

This execution will deploy to OSSRH and release to the Central Repository, thanks to the usage of the Nexus Staging Maven Plugin with autoReleaseAfterClose set to true.

### Create a Snapshot Branch with the Maven Release Plugin

Create new branch with next version, it won't update the working copy version:

```bash
mvn -B release:branch -DbranchName=my-branch -DupdateBranchVersions=true -DupdateWorkingCopyVersions=false 
```

### Manually Releasing the Deployment to the Central Repository

You can simply release the staging repository with

```bash
mvn nexus-staging:release -DautoReleaseAfterClose=true
```

If you have been running the deployment as part of a release done with the Maven release plugin, the deployment was done from the tag in your version control system checked out into target/checkout so you have to run the Nexus Staging plugin from there:

```bash
mvn release:perform
cd target/checkout
mvn nexus-staging:release
```

You can configure this goal to be run automatically as part of your release deployment with the release plugin by adding it as a goal execution after deploy.

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-release-plugin</artifactId>
  <configuration>
    <goals>deploy nexus-staging:release</goals>
  </configuration>
</plugin>
```

### Manually Publish the site to github pages

Publish to github pages:

```bash
mvn site scm-publish:publish-scm
```

## Links

Login to your [sonatype](https://s01.oss.sonatype.org/) account to release the version

| Type     | URL                                                                                                   | Description                |
|:---------|:------------------------------------------------------------------------------------------------------|:---------------------------|
| Snapshot | [sonatype](https://s01.oss.sonatype.org/content/repositories/snapshots/com/chensoul/chensoul-parent/) | Sonatype Snapshot versions |
| Release  | [maven](https://repo.maven.apache.org/maven2/com/chensoul/chensoul-parent/)                           | Maven Release versions     |
| Release  | [central-sonatype](https://central.sonatype.com/artifact/com.chensoul/chensoul-parent/)               | Sonatype Release versions  |


## References

- https://github.com/eclipse/microprofile
- https://github.com/microbean/microbean-parent
- https://github.com/naturalett/maven-hello-world/

## Documentation

Full documentation is, or will be, available at [chensoul.github.io/chensoul-parent](https://chensoul.github.io/chensoul-parent/).
