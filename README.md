### Sample Guide Maven Publish to CUBETIQ OSS Repository
###### For Java and Kotlin module for general Web Tech Stack

#### OSS Repository: [https://oss-internal.cubetiqs.com](https://oss-internal.cubetiqs.com)

#### Create gradle.properties in root project
```env
nexusUrl=https://oss-internal.cubetiqs.com
nexusUsername=yourUsername
nexusPassword=yourPassword
```

#### Config build.grdle in your project
```groovy
plugins {
    id 'java'
    id 'maven'
    ...
}

repositories {
    // For public version
    maven {
        url "${nexusUrl}/repository/maven-public/"
    }
    // For snapshot version
    maven {
        url "${nexusUrl}/repository/maven-snapshots/"
    }
    // For release version
    maven {
        url "${nexusUrl}/repository/maven-releases/"
    }
    ...
}

uploadArchives {
    repositories {
        mavenDeployer {
            repository(url: "${nexusUrl}/repository/maven-releases/") {
                authentication(userName: nexusUsername, password: nexusPassword)
            }
            snapshotRepository(url: "${nexusUrl}/repository/maven-snapshots") {
                authentication(userName: nexusUsername, password: nexusPassword)
            }
        }
    }
}

...
```
#### Publish the package
```shell
gradle upload
```
Or
```shell
./gradlew upload
```

#### Noted for Library Publish within GROUP ID
- For Snapshot version must be:
```groovy
group 'com.cubetiqs.libra'
version '1.0-SNAPSHOT'
```
- For Release version must be:
```groovy
group 'com.cubetiqs.libra'
version '1.0-RELEASE'
```
- For General/Normal version must be:
```groovy
group 'com.cubetiqs.libra'
version '1.0'
```

#### Noted for Module/Core Publish within GROUP ID
- For Snapshot version must be:
```groovy
group 'com.cubetiqs'
version '1.0-SNAPSHOT'
```
- For Release version must be:
```groovy
group 'com.cubetiqs'
version '1.0-RELEASE'
```
- For General/Normal version must be:
```groovy
group 'com.cubetiqs'
version '1.0'
```


#### Contributors
- Sambo Chea <sombochea@cubetiqs.com>

#### License
```text
Name: CUBETIQ Solution
Status: Commercial/OSS
```