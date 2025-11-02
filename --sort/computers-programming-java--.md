
[Apache Geronimo](https://geronimo.apache.org)

[GNU Classpath - GNU Project - Free Software Foundation (FSF)🆓](https://www.gnu.org/software/classpath)

[Java Expressions Library (JEL) home🆓](https://www.gnu.org/software/jel)

[Java Training Wheels - GNU Project - Free Software Foundation🆓](https://www.gnu.org/software/jtw)

[eleventigers/awesome-rxjava: Useful resources for working with RxJava](https://github.com/eleventigers/awesome-rxjava)
[GitHub - s0nerik/rxlist: Reactive List implementation using RxJava](https://github.com/s0nerik/rxlist)

[GitHub - jparams/data-store: Data Store is a full-featured indexed Java Collection capable of ultra-fast data lookup.](https://github.com/jparams/data-store)

[a-pavlov/jed2k: Java library for ed2k networks](https://github.com/a-pavlov/jed2k)

[GitHub - hosuaby/inject-resources: Simple and convenient way to read content of resource in Java.](https://github.com/hosuaby/inject-resources)

[findJAR](http://findjar.com/index.x)
a JAR search engine to help developers finding JAR libraries containing specific Java classes.

[Alex Zhitnitsky](http://blog.takipi.com/15-tools-to-use-when-deploying-code-to-production/)
(2014) 15 Tools Java Developers Should Use After a Major Release

[GitHub - markiewb/nb-resource-hyperlink-at-cursor: NetBeans Plugin which adds hyperlinks to filenames within String literals of Java sources](https://github.com/markiewb/nb-resource-hyperlink-at-cursor)

[GitHub - JCTools/JCTools](https://github.com/JCTools/JCTools)

[GitHub - stve/awesome-dropwizard](https://github.com/stve/awesome-dropwizard)
[Home — Dropwizard](https://www.dropwizard.io/en/stable/)

[Eclipse GlassFish](https://glassfish.org/)

## java - alternative JDK builds tools

[Home | Adoptium](https://adoptium.net/)

[Java Downloads | Oracle](https://www.oracle.com/java/technologies/downloads/)

[Java 7, 8, 11, 13, 15, 17, 19, 21 Download for Linux, Windows and macOS](https://www.azul.com/downloads/#zulu)

[OpenJDK Download - Corretto - AWS](https://aws.amazon.com/corretto/)

[Red Hat build of OpenJDK Download | Red Hat Developer](https://developers.redhat.com/products/openjdk/download)
[Microsoft Build of OpenJDK](https://www.microsoft.com/openjdk)

[Liberica JDK | Java runtime from an OpenJDK contributor](https://bell-sw.com/libericajdk/)

## java Apache Groovy tools

[GitHub - kdabir/awesome-groovy: A curated list of awesome groovy libraries, frameworks and resources](https://github.com/kdabir/awesome-groovy)

## java Apache Groovy reference and cheatsheets

[Jenkins Wiki](https://wiki.jenkins.io/display/JENKINS/Groovy+Hook+Script)
Groovy Hook Scripts

[Denny Zhang](https://cheatsheet.dennyzhang.com/cheatsheet-jenkins-groovy-a4)
(2018) CheatSheet: Jenkins & Groovy

[Groovy Docs](https://groovy-lang.org/syntax.html#_string_summary_table)
Syntax : String summary table

```
# List class methods
`<class>.metaClass.methods*.name.sort().unique()`

## Example
`println new Person().metaClass.methods*.name.sort().unique()`

Source http://groovy-almanac.org/list-the-methods-of-a-groovy-class/

# Print all object properties

## Method 1 ([src](https://gist.github.com/HopefulLlama/edecc82e9e6145544f34))

```groovy
println object.properties.sort{it.key}
.collect{it}
.findAll{!['class', 'active'].contains(it.key)}
.join('\n')
```

## Method 2 ([src](https://stackoverflow.com/questions/3069687/printing-out-variables-and-values-in-a-groovy-object))
`object.properties.each { println "$it.key -> $it.value" }`

## Method 3 ([src](https://stackoverflow.com/questions/3069687/printing-out-variables-and-values-in-a-groovy-object))
`object.dump().println()`
```
```

## java jvm tools

[Jacobin: A more than minimal JVM written in Go | Hacker News](https://news.ycombinator.com/item?id=37247394)
[Welcome to Jacobin JVM | jacobin](https://jacobin.org/)

[Lucee :: Accelerate your development with Lucee](https://www.lucee.org)

[CheerpJ 3.0: a JVM replacement in HTML5 and WASM to run Java on modern browsers | Hacker News](https://news.ycombinator.com/item?id=35873552)
[Announcing CheerpJ 3.0: A JVM replacement in HTML5 and WebAssembly to run Java applications (and applets) on modern browsers](https://labs.leaningtech.com/blog/announcing-cheerpj-3)

## references and cheatsheets

[John Hanley](http://www.javapractices.com/home/HomeAction.do)
Collected Java Practices

[Google](https://google.github.io/styleguide/javaguide.html)
Google Java Style Guide

[SSL Shopper](https://www.sslshopper.com/article-most-common-java-keytool-keystore-commands.html)
java keytool keystore cheatsheet
