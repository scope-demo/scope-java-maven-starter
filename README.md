# Scope: Getting Started

An starter Java project instrumented with [Scope](https://scope.undefinedlabs.com) through [GitHub Actions](https://github.com/features/actions).

This starter project is based on:
- [Java](https://www.java.com/en/download/)
- [Maven](https://maven.apache.org/)
- [Spring Boot 1.5](https://spring.io/projects/spring-boot)

## Install Scope on Maven projects with GitHub Actions

The project needs to add the `maven-surefire-plugin` and/or `maven-failsafe-plugin` in your `pom.xml` file.

```xml
<plugins>
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
    </plugin>
    
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-failsafe-plugin</artifactId>
        <executions>
            <execution>
                <goals>
                    <goal>integration-test</goal>
                    <goal>verify</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
</plugins>
```

Finally, the `scope-action-maven-jdk18` action has been configured in the GitHub Workflow `scope.yml` file:

```yaml
name: Scope Maven JDK v1.8
on: [push]

jobs:
  scope:
    runs-on: ubuntu-latest
    steps:
      - name: Check if SCOPE_APIKEY is set
        run: if [ "${{secrets.SCOPE_APIKEY}}" = "" ]; then exit 1; fi
      - uses: actions/checkout@v1
      - name: Run Scope Maven JDK 1.8
        uses: docker://undefinedlabs/scope-action-maven-jdk18:latest
        env:
          SCOPE_APIKEY: ${{secrets.SCOPE_APIKEY}}
```

For further information about how to install Scope, go to [Scope Java Agent Installation](https://docs.scope.dev/docs/java-installation)

## Running Scope on GitHub Actions

1. Click on `Use this template` button and create the repository in your namespace.
2. Access to [app.scope.dev](https://app.scope.dev) and 
3. Add/Modify your namespace to include your new repository.
4. Get the API Key for your new repository.
5. Go to your repository on [GitHub](https://github.com)
6. Go to `Settings` -> `Secrets`.
7. Add your API Key secret.
    - Name: `SCOPE_APIKEY`
    - Value: `<<your APIKEY>>`
8. Click on `Actions` button and access to the workflow.
9. Click on `Re-run checks`.

Once GitHub Workflow had finished, you can check the test executions report on [app.scope.dev](https://app.scope.dev) 
