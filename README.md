# Java Maven Template

A simple empty project with all the starter plugins and dependencies I use for my Java Maven projects. You don't have to use
what you don't need, but what's here probably won't hurt you.

If you see the word `voodoo` somewhere in this project, it's a property I'm pretty sure conveniences you, but I myself
have forgotten what it does or what use cases it affected.

## Maven

### [Maven Wrapper](https://maven.apache.org/wrapper/)

Allows a project to provide a fully encapsulated build setup.

##### Update the maven version used by the wrapper
```bash
MVNW_VERSION=<desired_maven_version>
```

```bash
./mvnw -N wrapper:wrapper -Dmaven=$MVNW_VERSION
```

### Profiles

#### Fast

Build with `./mvnw -Pfast` if you want to skip tests and all the code checks. It's useful if you're in the middle of
developing a new feature and need to just get a build working first.

This profile is auto-enabled in Intellij via
```xml
<activation>
    <property>
        <name>idea.maven.embedder.version</name>
    </property>
</activation>
```

## Code Quality Check Plugins

### [ErrorProne](https://errorprone.info/)

Error Prone is a static analysis tool for Java that catches common programming mistakes at compile-time. In addition to 
providing a ton of built-in rules, it's also highly customizable, allowing you to do things like enforce static imports
for specific libraries or force a specific package to be used over another.

When developing your own checks, you can use the [source code for built-in checks](https://github.com/google/error-prone/tree/21c190a6fc76f3ad3c895639dc66b7a3f570c55d/core/src/main/java/com/google/errorprone/bugpatterns) as an amazing reference for examples.

### [PMD](https://maven.apache.org/plugins/maven-pmd-plugin/)

**Currently disabled for not supporting Java 21**

Code analysis tool. Does a lot of what Errorprone does, but is more cumbersome to write. You can write rules using [XPath
processing](https://docs.pmd-code.org/pmd-doc-7.0.0-rc4/pmd_userdocs_extending_writing_xpath_rules.html) or as 
[Java rules](https://docs.pmd-code.org/pmd-doc-7.0.0-rc4/pmd_userdocs_extending_writing_java_rules.html).

In general, I consider PMD a last resort for super niche rules if they can't be done in Errorprone (not that I've found
an example of this yet).

Configured into the Maven build lifecycle with the [maven-pmd-plugin](https://maven.apache.org/plugins/maven-pmd-plugin/index.html).

All currently configured PMD rules in this project are example rules and can be chucked out if you find
its enforcement annoying or unnecessary.

#### Cross-Project Rules

A good practice to reuse rules across projects and across dev environments is to write your PMD rules and ruleset XML in
a separate project, and then build an artifact out of that project where the ruleset 
(e.g. `/resources/rulesets/java/pmd.xml`) is saved in the resources of the jar, and then add that artifact as a 
dependency of the `maven-pmd-plugin`.

```xml
<dependencies>
    <dependency>
        <groupId>com.icey7z</groupId>
        <artifactId>pmd-rules</artifactId>
        <version>1.0.0</version>
    </dependency>
</dependencies>
```

See the [official docs](https://pmd.github.io/pmd/pmd_userdocs_extending_writing_rules_intro.html) for guides on how to write your own rules

### [Checkstyle](https://checkstyle.org/)

Checkstyle is yet another static analysis tool. However, unlike PMD and Errorprone, Checkstyle is focused on coding style
conventions. Think of newlines at ends of files, files that are too long, formatting, and naming conventions. I would
recommend sharing a checkstyle configuration file between projects, and customizing the suppressions between them.

This project uses [Google's style guide](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml).

Configured into the Maven build lifecycle with the [maven-checkstyle-plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/index.html).

Checkstyle is configured in [checks/checkstyle.xml](checks/checkstyle.xml), and its suppressions are configured in
[checks/suppressions.xml](checks/checkstyle-suppressions.xml)


### [Gaul's Modernizer](https://gaul.github.io/modernizer-maven-plugin/index.html)

[Github](https://github.com/gaul/modernizer-maven-plugin)

Static analysis tool that searches your project for outdated or deprecated libraries and recommends replacements for
them. For instance, `joda -> java.time` 

### Tidy Maven POMs

### Macker

### Spotbugs


## Build Management Plugins

### Maven Enforcer

### Maven Dependency Scope

### Maven Resources

### [Maven Compiler](https://maven.apache.org/plugins/maven-compiler-plugin/)

Allows for more fine-grained control of the compilation process. The main motivation
for including this plugin is for integrating [Errorprone](#errorprone).

This plugin also allows you to use and configure the javac compiler with even more code checking functions via the `-Xlint`
arguments. You can also enable named parameters via `-parameters`, though I can't recall why I found this useful in the
past.

### Maven Source


## Dependency Management Plugins

### Maven Dependency Check

## Testing Plugins

### Surefire
TODO:
```xml
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.19.1</version>
        <configuration>
          <!-- set heap size to work around http://github.com/travis-ci/travis-ci/issues/3396 -->
          <argLine>-Xmx2g</argLine>
          <argLine>-Xmx2g --illegal-access=permit</argLine>
        </configuration>
      </plugin>
```
### Failsafe


## Notable Other Plugins not Included

Here are some situational plugins I've used in the past with great utility, but can't be recommended for all projects.

### Project13's Git Commit Id Plugin

### Spring Boot Maven Plugin

### Maven Exec

### Maven Shade

### Maven Antrun

### Maven Build Helper

## Testing

In addition to [Surefire]() and [Failsafe](), this project also comes rolled with [Jupiter JUnit 5]() and some examples on
how to roll your own Docker containers in tests as [JUnit Rules]().
