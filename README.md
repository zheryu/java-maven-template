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
./mvnw -N wrapper:wrapper -Dmaven=<desired_maven_version>
```

## Code Quality Check Plugins

### [ErrorProne](https://errorprone.info/)

Error Prone is a static analysis tool for Java that catches common programming mistakes at compile-time.




### PMD

### Checkstyle

### Gaul's Modernizer

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
how to roll your own Docker containers in tests as [Rules]().
