# Samers Script User Guide
A lot of the code in this repository is duplicated between applications.
Duplication is managed by the repository maintainers. The Samers script can be
used to facilitate this task. For an introduction to the repository, see the
[parent directory](..) readme file.

# Usage
The Samers script is a Python script. It is located in the
[samers.py](../Apps/samers.py) file.

You can run the script and get its usage like this, for example:

    cd /wherever/you/pulled/this/repository/IntegrationGuideForAndroid/Apps
    python3 ./samers.py -h

# Check the duplication status
The rules for which files should be duplicated are coded into the script. To
check the current status against the rules, run the following.

    python3 ./samers.py

Ignore the first two lines:

    Failed, no match for "nuffin".
    Failed, only one match for "samers*": samers.py.

Subsequent lines begin with either of the words OK or Differences. For example:

    OK 25 matches for "**/proguard-rules.pro".
    Differences "**/buildBase.gradle" "brandEnterprisePriorityExtendJava/buildBase.gradle"
        "TMPprivacyKotlin/buildBase.gradle"
    OK 22 matches for "**/integrateClient.gradle".
    Differences "**/integrateFramework.gradle" "brandEnterprisePriorityExtendJava/integrateFramework.gradle"
        "frameworkDelegateJava/integrateFramework.gradle"
    OK 11 matches for "**/src/**/AirWatchSDKIntentService.java".
    OK 11 matches for "**/src/**/AirWatchSDKIntentService.kt".
    ...

If all lines start OK then the duplication status is OK. Each line that begins
Differences represents a difference that must be resolved.

# Baling out
You can terminate the script safely and at any time by pressing Ctrl-C.

# Apply a file update
One way to resolve a difference is to copy a file over other files that are
supposed have the same contents. This is a typical case during the updating
procedure for a new version of the Workspace ONE software development kit for
Android.

For example, suppose updates to the integrateFramework.gradle file are required.
The typical procedure would be to update one copy and verify the updates by
building and running the app that is built with it. Then the update has to be
applied to all the other copies of the integrateFramework.gradle file.

To overwrite all files that are supposed to be the same as an updated file, run
the following.

    python3 ./samers.py -v path/to/the/updated.File

For each file that should be the same but is different, this will show the
differences, and prompt you to overwrite. The prompt looks like this for each
file:

    $ python3 ./samers.py -v frameworkDelegateJava/integrateFramework.gradle 
    frameworkDelegateJava/integrateFramework.gradle
    Matches "**/integrateFramework.gradle":
        Different "brandEnterprisePriorityExtendJava/integrateFramework.gradle"
    *** frameworkDelegateJava/integrateFramework.gradle
    --- brandEnterprisePriorityExtendJava/integrateFramework.gradle
    ***************
    *** 31,41 ****
        implementation(name:'AWComplianceLibrary-2.3.5', ext: 'aar')
        implementation(name:"AWFramework-${airwatchVersion}", ext: 'aar')
        implementation(name:'VisionUx-1.5.0.a', ext: 'aar')
    !   implementation(name:'CredentialsExt-102.1.0', ext: 'aar')
        implementation(name:"chameleon-android-1.0.16-ndk-r21c", ext:'aar')
        implementation(name:"settings-1.0.17-ndk-r21c", ext:'aar')
        implementation(name:"opdata-android-1.3.2", ext:'aar')
    !   implementation(name:"attributesprovider-1.0.17-ndk-r21c", ext:'aar')
        implementation(name:"encryptedpreferencesprovider-1.0.12", ext:'aar')
        implementation(name:"httpprovider-1.0.11", ext:'aar')
        implementation(name:"memoryprovider-1.0.11", ext:'aar')
    --- 31,41 ----
        implementation(name:'AWComplianceLibrary-2.3.5', ext: 'aar')
        implementation(name:"AWFramework-${airwatchVersion}", ext: 'aar')
        implementation(name:'VisionUx-1.5.0.a', ext: 'aar')
    !   implementation(name:'CredentialsExt-101.1.0', ext: 'aar')
        implementation(name:"chameleon-android-1.0.16-ndk-r21c", ext:'aar')
        implementation(name:"settings-1.0.17-ndk-r21c", ext:'aar')
        implementation(name:"opdata-android-1.3.2", ext:'aar')
    !   implementation(name:"attributesprovider-1.0.17", ext:'aar')
        implementation(name:"encryptedpreferencesprovider-1.0.12", ext:'aar')
        implementation(name:"httpprovider-1.0.11", ext:'aar')
        implementation(name:"memoryprovider-1.0.11", ext:'aar')

        Overwrite? (Y/n/?)

In the differences portion, the first set of lines are always from the file that
was specified on the command line. The second set are from a file that should
have the same contents. Check that the first set is what's required and key
return to overwrite. If the first set aren't what's required then type n and
return. The overwrite of that file will then be skipped.

# Other tasks
Other tasks are TBD at this time, sorry.

# License
Copyright 2020 VMware, Inc. All rights reserved.  
The Workspace ONE Software Development Kit integration samples are licensed
under a two-clause BSD license.  
SPDX-License-Identifier: BSD-2-Clause