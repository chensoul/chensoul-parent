# ChenSoul™: Parent POM

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.chensoul/chensoul-parent)

This project houses the parent Project Object Model (POM) for most ChenSoul™ projects.

## Links

Login to your [sonatype](https://s01.oss.sonatype.org/) account to release the version

| Type     | URL                                                                                                   | Description       |
|:---------|:------------------------------------------------------------------------------------------------------|:------------------|
| Snapshot | [sonatype](https://s01.oss.sonatype.org/content/repositories/snapshots/com/chensoul/chensoul-parent/) | Snapshot versions |
| Release  | [sonatype](https://repo.maven.apache.org/maven2/com/chensoul/chensoul-parent/)                        | Release versions  |
| Release  | [central-sonatype](https://central.sonatype.com/artifact/com.chensoul/chensoul-parent/1.0.0/versions) | Release versions  |

## Secrets

* **MAVEN_GPG_PRIVATE_KEY** - Take it from the private.gpg
* **OSSRH_USERNAME** - Created [here](https://issues.sonatype.org/)
* **OSSRH_TOKEN** - Created [here](https://issues.sonatype.org/)
* **MAVEN_GPG_PASSPHRASE** - Create [here](https://central.sonatype.org/publish/requirements/gpg/#generating-a-key-pair)
    * This passphrase and your private key are all that is needed to sign artifacts with your signature.
* **GITHUB_TOKEN** - Github token

## Demo

How do you release a version?

Manually:\
&nbsp;&nbsp;&nbsp;1. Check the version in the pom.xml\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* **<version>1.0.0-SNAPSHOT</version>**\
&nbsp;&nbsp;&nbsp;2. Go to Github action -> Run workflow\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* **Release:** 1.0.0\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* **Snapshot:** 1.0.1-SNAPSHOT

Automatically:\
Push to Github will create a release and a snapshot but it won't publish the release.\
Snapshot will be available through [here](https://central.sonatype.com/artifact/com.chensoul/chensoul-parent/1.0.0)

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

## Local commands

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

Release and deploy to maven repository:

```bash
mvn -B release:clean release:prepare release:perform
```

Update pom version:

```bash
mvn -B build-helper:parse-version versions:set -DnewVersion=1.0.0-SNAPSHOT versions:commit 
```

Create new branch with next version, it won't update the working copy version:

```bash
mvn -B release:branch -DbranchName=my-branch -DupdateBranchVersions=true -DupdateWorkingCopyVersions=false
```

GPG to sign and deploy to sonatype repository using release profile:

```bash
mvn -B clean deploy -Prelease -Dgpg.passphrase=<PASSPHRASE_GPG> -Dusername=<OSSRH_USERNAME> -Dpassword=<OSSRH_TOKEN>

# reading gpg.passphrase, username and password from settings.xml
mvn -B clean deploy -Prelease
```

## Authors

- [@chensoul](https://www.github.com/chensoul)

## Thanks

- https://github.com/microbean/microbean-parent
- https://github.com/naturalett/maven-hello-world
