# Maven

## Manage dependencies

* `mvn versions:display-dependency-updates` to detect updates.
* `mvn versions:display-property-updates` to precisely monitor the latest dependencies and their version..
* `mvn versions:use-latest-versions` to force the change of the versions by the last ones.

## Check the weaknesses

To know the weaknesses of your expenses, can help
this [DependencyCheck tool](https://jeremylong.github.io/DependencyCheck/)

```
        <plugin>
              <groupId>org.owasp</groupId>
              <artifactId>dependency-check-maven</artifactId>
              <version>${owasp}</version>
              <executions>
                  <execution>
                      <goals>
                          <goal>check</goal>
                      </goals>
                  </execution>
              </executions>
            </plugin>
```

As result by running ` mvn verify` or `mvn install`  you will obtain a table listing the CVE associated with your
dependencies.

# Gradle

* `./gradle init` to create a new Gradle project via wizard.

## Tasks 
* `./gradlew tasks` to see all available tasks
* `./gradlew build` to build via Gradle Wrapper
* `./gradlew clean` to clean `build` folders
* `./gradlew test` to run tests, `build\reports\tests` folder contains test report.
* `./gradlew test -p SUBMODULE_FOLDER\` to run tests only in `SUBMODULE_FOLDER`

## Structure

```
|—— build.gradle
|—— gradle
    |—— wrapper
        |—— gradle-wrapper.jar
        |—— gradle-wrapper.properties
|—— gradlew
|—— gradlew.bat
|—— settings.gradle
```
- file `settings.gradle` sets project name, and etc.
    - `type settings.gradle` to see the setting via Windows-cmd
- file `./gradlew`(Linux/Mac) and `gradlew.bat`(Windows) to execute via Gradle Wrapper
- folder `gradle` contains wrapper
- hidden folder `.gradle` is local Gradle cache(should not be commited)
- file `build.gradle` main Gradle build script file, it presents in every module.

## Tricks

### Reference to another module

`implementation project(':my-backend')` to reference ot another module in the existing project.


### Transitive dependencies

* `java`-plugin doesn't understand `api` scope
* `java-library`-plugin is required to operate with `api` scope
* `api` scope allows to add the dependencies transitively

