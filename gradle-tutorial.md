# Gradle Tutorial

## Install Gradle

1. Get `sdkman`:

   ```bash
   curl -s "https://get.sdkman.io" | bash
   source "$HOME/.sdkman/bin/sdkman-init.sh"
   ```

2. Install Gradle with `sdkman`

   ```bash
   sdk install gradle
   ```

## Initialize a new Java/Groovy Project

```
mkdir demo-app && cd demo-app
gradle init --project-name demo-app --type groovy-application --package com.demo --dsl groovy
./gradlew run
```

## Build an All-in-One JAR File for the Project

Install `Shadow` Gradle plugin with following changes in `build.gradle` file:

```groovy
plugins {
    // Apply the Shadow plugin to build a "fat-jar" artifact
    id 'com.github.johnrengelman.shadow' version '4.0.3'
}
```

After running `./gradlew build` a uber JAR file will be created in `build/lib/` directory. The name of the JAR file is the same as project name, which is configurable in `settings.gradle` file.

## Enable to Run a Java/Groovy Class from `gradlew` Command

Make the following changes in the `build.gradle` file:

```groovy
// Define the main class for the application
mainClassName = 'com.demo.App'

// Enabling to run app by its class name
task runApp(type: JavaExec) {
    classpath = sourceSets.main.runtimeClasspath
    main = project.hasProperty('mainClass') ? project.getProperty('mainClass') : mainClassName
}
```

## Display Detailed Output During Testing

Make the following changes to the `build.gradle` file:

```
test {
	//we want display the following test events
    testLogging {
        // events "PASSED", "STARTED", "FAILED", "SKIPPED"
        events "PASSED", "FAILED"
    }
}
```
