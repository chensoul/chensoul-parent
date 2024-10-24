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
    <version>1.1.9</version>
    <relativePath/>
</parent>
```
