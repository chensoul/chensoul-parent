# ChenSoul Parent POM

<p align="center">
  <a href="https://search.maven.org/artifact/com.chensoul/chensoul-parent">
    <img alt="maven" src="https://img.shields.io/maven-central/v/com.chensoul/chensoul-parent.svg?style=flat-square"/>
  </a>

  <a href="https://www.apache.org/licenses/LICENSE-2.0">
    <img alt="code style" src="https://img.shields.io/badge/license-Apache%202-4EB1BA.svg?style=flat-square"/>
  </a>
</p>


Chensoul 项目的父级 POM，用于管理项目的依赖和插件版本，目前仅适用于 JDK 1.8。

## 使用

在 [Maven Central](https://search.maven.org/artifact/com.chensoul/chensoul-parent) 上可以找到 ChenSoul™ Parent POM
的最新版本。使用 ChenSoul™ Parent POM 作为 Maven 的父级 POM：

```xml

<parent>
    <groupId>com.chensoul</groupId>
    <artifactId>chensoul-parent</artifactId>
    <!-- https://search.maven.org/artifact/com.chensoul/chensoul-parent -->
    <version>1.0.0</version>
    <relativePath/>
</parent>
```

## 生成 GPG 密钥

参考 [这里](https://central.sonatype.org/publish/requirements/gpg/#generating-a-key-pair) 生成 GPG 密钥。

```bash
gpg --full-generate-key

gpg --list-secret-keys --keyid-format=long

gpg --armor --export-secret-keys <YOUR_KEY> > private.gpg

gpg --keyserver hkp://keyserver.ubuntu.com:11371 --send-keys <YOUR_KEY>

gpg --export xxx@xxx.com > my_key.pub
```

## 如何发布到 Sonatype 仓库

1. 首先配置 `～/.m2/settings.xml`:

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

- 生成 ossrh token，请参考 https://central.sonatype.org/publish/generate-token/#alternatives-to-removal-or-modification-of-components

2. 发布快照版本到快照仓库 https://s01.oss.sonatype.org/content/repositories/snapshots/

```bash
mvn -B clean source:jar javadoc:jar deploy
```

3. 发布正式版本到正式仓库

首先，修改版本号为正式版本号：

```bash
mvn versions:set -DnewVersion=1.2.3 versions:commit
```
然后，执行发布命令：

```bash
mvn clean source:jar javadoc:jar deploy
```

然后，登录 https://s01.oss.sonatype.org/#stagingRepositories ，手动关闭 staging 参考，然后发布。

稍等几分钟，可以在以下仓库查看发布的 jar:
- https://central.sonatype.com/artifact/com.chensoul/chensoul-parent/
- https://s01.oss.sonatype.org/service/local/repositories/releases/content/com/chensoul/chensoul-parent/
- https://repo.maven.apache.org/maven2/com/chensoul/chensoul-parent/

## 上传网站到 github-pages

```bash
mvn clean site scm-publish:publish-scm
```

## 参考文章

- [GPG](https://central.sonatype.org/publish/requirements/gpg/)



