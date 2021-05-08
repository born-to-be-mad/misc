# Maven

## Manage dependencies

* `mvn versions:display-dependency-updates ` to detect updates.
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
