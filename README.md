## Prospero metadata

This project is part of [Prospero project](https://github.com/wildfly/prospero/) and provides the API to create the installation metadata used by Prospero to manager and update WildFly servers.

## Building

* JDK 11 or newer - check `java -version`
* Maven 3.6.0 or newer - check `mvn -v`

To build with your own Maven installation:

    mvn install

## Release Procedure

# Releasing Remoting JMX

Prior to releasing you should ensure you have your own GPG signing key set up, published to a key server and listed on [wildfly.org](https://www.wildfly.org/contributors/pgp/).

## Prepare the release

Execute:

```
mvn release:prepare -Pjboss-release
```

## Perform the release

Execute:

```
mvn release:perform -Pjboss-release
```

This will deploy the release to the `wildfly-staging` repository.

Wait for 10 minutes then visit the Validation task for the [`wildfly-staging` repository in Nexus](https://repository.jboss.org/nexus/#browse/browse:wildfly-staging). If this task ran at least 10 minutes after the release was deployed check the latest results on the Settings tab and verify that at least one component was processed and that there were no errors. If the task has not run it can be manually kicked off using the Run button.

e.g.

> Processed X components.
> - no errors were found.
> - the deployment was a dry run (no actual publishing).

If others are also deploying at the same time this count could be higher, the important check is that the scan was at least 10 minutes after it was deployed, 1 or more components were scanned and no errors specific to Remoting JMX are reported.

## Complete the release

If no issues are reported complete the release.

Move the component to the releases repository:

```
git checkout <tag of the release>
mvn nxrm3:staging-move
```

Once this is done, the release will be pushed to the `releases` repository in Nexus and then to Maven Central.
## License

* [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)
