# androidcommon

This project is __*actively maintained*__

It is part of the ODK-X Android tools suite.

This is a library APK used by all the ODK-X Android tools.

The developer [wiki](https://github.com/odk-x/tool-suite-X/wiki) (including release notes) and
[issues tracker](https://github.com/odk-x/tool-suite-X/issues) are located under
the [**ODK-X Tool Suite**](https://github.com/odk-x) project.

Engage with the community and get technical support on [the ODK-X forum](https://forum.odk-x.org)


## Build Status

*master* | *demo* | *development*
-------- | ------ | -------------
[![Build Status](http://cwe.cs.washington.edu:8081/buildStatus/icon?job=master-androidcommon)](http://cwe.cs.washington.edu:8081/view/ODK%20Full%20Release/job/master-androidcommon/) | [![Build Status](http://cwe.cs.washington.edu:8081/buildStatus/icon?job=demo-androidcommon)](http://cwe.cs.washington.edu:8081/view/ODK%20Soft%20Release/job/demo-androidcommon/) | [![Build Status](http://cwe.cs.washington.edu:8081/buildStatus/icon?job=androidcommon)](http://cwe.cs.washington.edu:8081/job/androidcommon/)

## Branch Structure

There are three branches in our git workflow:
* *master* is where fully released and **stable** code lives. Changes flow into this branch from demo. Each merge correponds with an official release or a hot fix.
* *demo* is where **beta** versions are tested before release and also where we hold demo or preview versions of upcoming releases and new features. This branch is more stable than development but should still only be used for testing purposes. Changes flow into this branch from development.
* *development* is where new features and code changes are made. This branch is the bleeding edge and is **not stable**. It should only be used for development and testing purposes. If you want to submit a pull request, please do it against *development*.

## Setting up your environment and building the project

General instructions for setting up an ODK 2.0 environment can be found at our [DevEnv Setup wiki page](https://github.com/opendatakit/opendatakit/wiki/DevEnv-Setup)

Install [Android Studio](http://developer.android.com/tools/studio/index.html) and the [SDK](http://developer.android.com/sdk/index.html#Other).

This project depends on the ODK [androidlibrary](https://github.com/opendatakit/androidlibrary) project; its binaries will be downloaded automatically fom our maven repository during the build phase. If you wish to modify that project, you must clone it into the same parent directory as androidcommon. You directory stucture should resemble the following:

        |-- odk

            |-- androidcommon

            |-- androidlibrary


  * Note that this only applies if you are modifying androidlibrary. If you use the maven dependencies (the default option), the project will not show up in your directory. 

Open the androidcommon project directory in Android Studio.

Now you should be ready to build, by selecting `Build->Make Project`.

Alternatively, you can build from the command line using Gradle. From the root directory of this project, run:

`gradlew clean assemble`

For more details see the [Gradle documentation for Andoid](https://guides.gradle.org/building-android-apps/).

## Running

**NOTE** this project will NOT run on an Android device by itself, it is simply a library for use in other ODK projects.

## Downloading Binaries

You can use ivy (for the *development* and *demo* branches) and maven (for the *master* branch) to access prebuilt binaries within your project. Your build.gradle file might look like this:
```
allprojects {
    repositories {
        jcenter()
        ivy {
            url 'http://cwe.cs.washington.edu:8082/artifactory/libs-demo/'
        }
        maven {
            url 'http://cwe.cs.washington.edu:8082/artifactory/libs-master/'
        }
        ivy {
            url 'http://cwe.cs.washington.edu:8082/artifactory/libs-snapshot/'
        }
    }
}

```

We are already doing this in our other projects such as our root build.gradle file in [Services](https://github.com/opendatakit/services/blob/master/build.gradle). 

Each commit to the *development* branch is built and published to our Artifactory server's [snapshot library](http://cwe.cs.washington.edu:8082/artifactory/webapp/builds/androidcommon/?2). They can be identified by their git hash in their versioning. They are also linked between our Jenkins build server and Artifactory by build number. 

Furthermore, each beta version published to the *demo* branch is published to our Artifactory server's [demo library](http://cwe.cs.washington.edu:8082/artifactory/webapp/builds/demo-androidcommon/?4) and similarly linked to the Jenkins build server.

Finally, each release version published to the *master* branch is published to our Artifactory server's [master library](http://cwe:8082/artifactory/webapp/browserepo.html?2). However, these are NOT built by Jenkins; they are built and tested by hand for the release.


## How to contribute
If you’re new to ODK-X you can check out the documentation:
- [https://docs.odk-x.org](https://docs.odk-x.org)

Once you’re up and running, you can choose an issue to start working on from here: 
- [https://github.com/odk-x/tool-suite-X/issues](https://github.com/odk-x/tool-suite-X/issues)

If you're writing tests, we use JaCoCo for test coverage reporting. This is already included in [gradle-config](https://github.com/odk-x/gradle-config)

Issues tagged as [good first issue](https://github.com/odk-x/tool-suite-X/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) should be a good place to start.

Pull requests are welcome, though please submit them against the development branch. We prefer verbose descriptions of the change you are submitting. If you are fixing a bug please provide steps to reproduce it or a link to a an issue that provides that information. If you are submitting a new feature please provide a description of the need or a link to a forum discussion about it. 

## Running test coverage
- Clone [gradle-config](https://github.com/odk-x/gradle-config) into your local repo's parent folder
- Build the project and ensure success.
- Run coverage with `./gradlew createSnapshotDebugUnitTestCoverageReport`.
- Then, follow the provided filepath to view the report.

## Links for users
This document is aimed at helping developers and technical contributors. For information on how to get started as a user of ODK-X, see our [online documentation](https://docs.odk-x.org), or to learn more about the Open Data Kit project, visit [https://odk-x.org](https://odk-x.org).
