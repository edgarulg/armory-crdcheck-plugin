![CI](https://github.com/spinnaker-plugin-examples/pf4jStagePlugin/workflows/CI/badge.svg)
![Latest Kork](https://github.com/spinnaker-plugin-examples/pf4jStagePlugin/workflows/Latest%20Kork/badge.svg?branch=master)
![Latest Orca](https://github.com/spinnaker-plugin-examples/pf4jStagePlugin/workflows/Latest%20Orca/badge.svg?branch=master)

This plugin helps to determinate if a CRD is stable or not.

# Version Compatibility
 
| Plugin  | Spinnaker Platform | Armory Spinnaker Platform
|:----------- | :--------- | :---------
| 0.0.17  |  1.19.x & 1.20.x | 2.20.x
| 0.1.2  |  1.21.x | 2.21.x

# Usage

1) Run `./gradlew releaseBundle`
2) Put the `/build/distributions/<project>-<version>.zip` into the [configured plugins location for your service](https://pf4j.org/doc/packaging.html).
3) Configure the Spinnaker service. Put the following in the service yml to enable the plugin and configure the extension:

```
spinnaker:
  extensibility:
    plugins:
      Armory.CRDCheck:
        enabled: true
        version: 0.1.2
        extensions: {}
```

Or use the [examplePluginRepository](https://github.com/spinnaker-plugin-examples/examplePluginRepository) to avoid copying the plugin `.zip` artifact.

# Debugging

To debug the `crdcheck-clouddriver`  server component inside a Spinnaker service (like Clouddriver) using IntelliJ Idea follow these steps:

1) Run `./gradlew releaseBundle` in the plugin project.
2) Copy the generated `.plugin-ref` file under `build` in the plugin project submodule for the service to the `plugins` directory under root in the Spinnaker service that will use the plugin .
3) Link the plugin project to the service project in IntelliJ (from the service project use the `+` button in the Gradle tab and select the plugin build.gradle).
4) Configure the Spinnaker service the same way specified above.
5) Create a new IntelliJ run configuration for the service that has the VM option `-Dpf4j.mode=development` and does a `Build Project` before launch.
6) Debug away...
