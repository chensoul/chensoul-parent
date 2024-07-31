# ChenSoul Parent POM

<p align="center">
  <a href="https://search.maven.org/artifact/com.chensoul/chensoul-parent">
    <img alt="maven" src="https://img.shields.io/maven-central/v/com.chensoul/chensoul-parent.svg?style=flat-square"/>
  </a>

  <a href="https://www.apache.org/licenses/LICENSE-2.0">
    <img alt="code style" src="https://img.shields.io/badge/license-Apache%202-4EB1BA.svg?style=flat-square"/>
  </a>
</p>


Chensoul 项目的父级 POM，用于管理项目的依赖和插件版本，目前适用于 JDK 8、11、17、21。

## 使用

在 [Maven Central](https://search.maven.org/artifact/com.chensoul/chensoul-parent) 上可以找到 ChenSoul™ Parent POM
的最新版本。使用 ChenSoul™ Parent POM 作为 Maven 的父级 POM：

```xml

<parent>
    <groupId>com.chensoul</groupId>
    <artifactId>chensoul-parent</artifactId>
    <version>1.1.1</version>
    <relativePath/>
</parent>
```

## 生成 GPG 密钥

参考 [这里](https://central.sonatype.org/publish/requirements/gpg/#generating-a-key-pair) 生成 GPG 密钥。

```bash
gpg --gen-key

gpg --list-secret-keys --keyid-format=long

gpg --armor --export-secret-keys <YOUR_KEY> > private.gpg

# keyserver.ubuntu.com
# keys.openpgp.org
# pgp.mit.edu
gpg --keyserver keys.openpgp.org --send-keys <YOUR_KEY>

gpg --export xxx@xxx.com > my_key.pub
```

## 发布到 Sonatype 仓库

1. 生成 sonatype token
   请参考 https://central.sonatype.org/publish/generate-token/#alternatives-to-removal-or-modification-of-components

2. 配置 `～/.m2/settings.xml`:

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

2. 发布快照

```bash
mvn -B -P release clean deploy
```

执行成功之后，访问 https://s01.oss.sonatype.org/content/repositories/snapshots/com/chensoul/chensoul-parent/ 查看发布的 jar。

3. 发布正式版本到正式仓库

首先，修改版本号为正式版本号：

```bash
mvn versions:set -DnewVersion=1.1.0 versions:commit
```
然后，执行发布命令：

```bash
mvn -B -P release clean deploy
```

执行成功之后，稍等几分钟，可以在以下仓库查看发布的 jar:
- https://central.sonatype.com/artifact/com.chensoul/chensoul-parent/
- https://s01.oss.sonatype.org/service/local/repositories/releases/content/com/chensoul/chensoul-parent/
- https://repo.maven.apache.org/maven2/com/chensoul/chensoul-parent/

4. 使用 Github Actions 发布

参考 https://quentincastel86.medium.com/release-your-maven-project-using-github-actions-51beba1e4834

## 上传网站到 github-pages

参考 [将 Maven 站点发布到 GitHub Pages](https://blog.chensoul.cc/posts/2024/07/18/publishing-a-maven-site-to-github-pages/)，首先配置 `~/.m2/settings.xml`:

```bash
<server>
    <id>github</id>
    <username>chensoul</username>
    <password>ghp_XXXXXXXXXXXXXXXXX</password>
</server>
```

发布网站到 github pages：

```bash
mvn -ntp -B -U clean site scm-publish:publish-scm -Dscmpublish.serverId=github
```

## 参考文章

- [GPG](https://central.sonatype.org/publish/requirements/gpg/)
- https://medium.com/@alexander.volminger/ci-cd-for-java-maven-using-github-actions-d009a7cb4b8f
