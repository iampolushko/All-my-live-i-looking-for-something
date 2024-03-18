# Maven

## Download and configure

use it jus for download

```
mvn install
```

```
mvn compiler:compile
```

```
mvn org.apache.maven.plugins:maven-compiler-plugin:compile
```

```
mvn org.apache.maven.plugins:maven-compiler-plugin:2.0.2:compile
```

for safety build and rebuild docs

```
mvn clean compile assembly:single
```

## important fckng facts

- if u wanna use any fckn file (sqlite too) u should add it in resource folder
- Check the windows pre installed java jdk
- Maven what you installed on windows and maven in idea it is different programs

*

## pom.xml

- ### group id
  Here we got the pachage name.
- ### artificalId
  artifact - is anything what you got after comiling(program, lib or something)
- ### version

# From jar to exe

## Launch4j

### Tips:

- If you choose the stock JRE(windows variable PATH) you should mark the min JRE version.
- If u faggot! Create the new directory in the resoult exe file directory and add all JDK folder files and print the inside directory name in "JRE PATH".
