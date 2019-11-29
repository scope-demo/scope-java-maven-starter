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

Finally, the `scope-for-maven-action` action has been configured in the GitHub Workflow `scope.yml` file:

```yaml
name: Scope Maven JDK v1.8
on: [push]

jobs:
  scope:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
      - name: Set up JDK 1.8
        uses: actions/setup-java@v1
        with:
          java-version: 1.8 
      - name: Scope for Maven Action
        uses: undefinedlabs/scope-for-maven-action@v1
        with:
          dsn: ${{secrets.SCOPE_DSN}}
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
    - Name: `SCOPE_DSN`
    - Value: `https://<<your APIKEY>>@app.scope.dev`
8. Click on `Actions` button and access to the workflow.
9. Click on `Re-run checks`.

Once GitHub Workflow has finished, you can check the test executions report on [app.scope.dev](https://app.scope.dev) 
