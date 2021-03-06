# Integration Preparation Guide
## Workspace ONE for Android
Android applications can be integrated with the VMware Workspace ONE® platform,
by using its mobile software development kit. Complete the tasks below to
prepare for integration.

This document is part of the Workspace ONE Integration Guide for Android set.

# Table of Contents
{{TOC}}

# Introduction
The tasks detailed below should be done first, to prepare for integration of
your Android application with the Workspace ONE platform. After completing these
tasks, you will be ready to begin the integration.

## Integration Guides
This document is part of the Workspace ONE Integration Guide for Android set. An
overview that includes links to all the guides is available

-   in Markdown format, in the repository that also holds the sample code:  
    [https://github.com/vmware-samples/...IntegrationOverview.md](https://github.com/vmware-samples/workspace-ONE-SDK-integration-samples/blob/main/IntegrationGuideForAndroid/Guides/01Overview/WorkspaceONE_Android_IntegrationOverview.md)

-   in Portable Document Format (PDF), on the VMware website:  
    [https://code.vmware.com/...IntegrationOverview.pdf](https://code.vmware.com/docs/12354/WorkspaceONE_Android_IntegrationOverview.pdf)

# Prerequisites [prerequisite conditions]
Before you begin, you will need the following.

-   Access to a Workspace ONE management console.

    You will need access to a Workspace ONE management console to work on
    application integration. The management console is sometimes referred to as
    the UEM, an abbreviation for Unified Endpoint Manager.

    You will need to know the following:

    -   Server address.
    -   Administrative login credentials.

    You will need the following privileges:

    -   Upload an application package (APK) file.
    -   Either create an organisation group for an end user, or get the name of
        an existing group.
    -   Either create a new end user with a suitable profile for development
        purposes, or get the name of an existing suitable user.
    -   Either create enrolment credentials for an end user, or get existing
        credentials.

    Best practice is to have a separate console, or organisation group, for 
    software development.

    Check the [Compatibility] table for a recommended version.

-   Developer environment.

    The instructions in the integration guide documents assume you use the
    Android Studio integrated developer environment (IDE). Check the
    [Compatibility] table for a recommended version.

-   Android application source code.

    Integrating an application with Workspace ONE will involve changes to the
    application source code. You will need access to the Java or Kotlin source,
    to the manifest and resources, and to any other files required to build the
    application.

    You can integrate Workspace ONE with an existing Android application of your
    own, or with an Android sample application, or start a new application from
    an Android Studio template, for example.

    The instructions in the integration guide documents assume your application
    uses AndroidX instead of the original support library. Instructions for
    migrating from the support library to AndroidX can be found on the Android
    developer website, for example here:  
    [https://developer.android.com/jetpack/androidx/migrate](https://developer.android.com/jetpack/androidx/migrate)

-   Developer device.

    You will need a physical Android device to to work on application
    integration.
    
    The Android emulator cannot be used because emulated devices may appear as
    rooted or otherwise compromised to the Workspace ONE Intelligent Hub
    application. The Hub must be used to install the application that is being
    integrated at least once during the integration work.

    After the first installation via Hub, subsequent installations can be made
    using the Android Debug Bridge (adb) tool. The device must be set up for
    developer use. Instructions for setting up a developer device can be found
    on the Android developer website, for example on the following pages.
    
    -   [https://developer.android.com/studio/debug/dev-options.html](https://developer.android.com/studio/debug/dev-options.html)
    -   [https://developer.android.com/studio/run/device](https://developer.android.com/studio/run/device)

    Don't use a device that is already enrolled with a production Workspace ONE
    console. A device can be unenrolled by removing or resetting the Hub
    application on the device, and uninstalling any associated applications.

When the prerequisite conditions are met, you can start the first task, which is
to [install your application via Workspace ONE].

## Compatibility
Instructions in this document have been followed with the Workspace ONE Software
Development Kit (SDK) for Android and other software, to confirm compatibility.

The following table shows the software versions used for the instructions, and
the minimum supported versions if different.

Software                                           | Instructions | Supported |
---------------------------------------------------|--------------|-----------|
Workspace ONE software development kit for Android | 20.10        |           |
Workspace ONE management console                   | 20.4         | 1904      |
Workspace ONE Intelligent Hub application          | 20.09        | 19.07     |
Android API level                                  | 29           | 19        |
Android Studio integrated development environment  | 4.1          | 3.3       |
Gradle plugin for Android                          | 4.1          | 3.3       |

# Task: Install application via Workspace ONE [install your application via Workspace ONE]
Installing the application via Workspace ONE is a platform integration task for
Android application developers. It applies to all levels of platform
integration.

## Installation Order
If you follow the integration guide, you will install your application on a
developer device as follows.

-   The first installation will be of a non-integrated version of the
    application via Workspace ONE, by following the instructions below.

-   Subsequent installations will be of integrated versions of the application,
    via the Android Debug Bridge (adb) tool.

The adb installations will be upgrades. The application won't ever be
uninstalled after the first installation via Workspace ONE.

It actually isn't necessary to install an application via Workspace ONE if it
isn't integrated. It might therefore seem natural to delay installation via
Workspace ONE until some integration work has been done. This guide doesn't
follow that order though.

The rationale is that installation via Workspace ONE involves activities with
which you may be unfamiliar, such as setting up signed builds, and use of the
Workspace ONE management console. It's better to do those activities with the
application in a known working state.

## Instructions
The instructions assume that the [prerequisite conditions] are all met.

Proceed as follows.

1.  Install and enrol the Hub application.

    Install the Workspace ONE Intelligent Hub application on the device and
    complete enrolment. The Hub can be installed from Google Play. Search for
    "workspace one intelligent hub", for example.

    Follow the instructions in the Hub application to complete enrolment. You
    will need to know the server address and a set of end user enrolment
    credentials.

    **Tip**: Set a device passcode before you begin enrolment. Typical UEM
    configurations will require a passcode, as a security policy. If a device
    passcode isn't set at the start of the enrolment interaction, you will be
    forced to  set it as an enrolment step, which sometimes doesn't go smoothly.

    **Warning**: The Hub application cannot be enrolled with more than one
    management console at a time. If the Hub is already installed and enrolled
    on your developer device, then it must now be removed and re-installed, or
    must be reset, i.e. have its storage cleared. Removing or resetting the Hub
    may cause removal of any associated applications from the device.

    Check the [Compatibility] table for a recommended version of Hub.

2.  Generate a signed package file for your application.

    You will need a signed Android package (APK) file for your application. A
    signed APK can be generated by Android Studio. See the
    [How to generate a signed Android package every build] instructions in this
    document, if needed.

    Note that you don't need to do any Workspace ONE integration in the
    application at this stage.

    You can use any key store to sign the APK, even one you create ad hoc now.
    You don't have to use the same key your organisation uses to sign APK files
    for production.

3.  Upload your application to the management console.

    Upload the APK file from the previous step to the Workspace ONE management
    console.

    See the [How to upload an Android application to the management console]
    instructions in this document, if needed.

    The signing details from the uploaded APK will be used by the Hub for
    verification going forwards.

4.  Install your application from Hub.

    Your application can now be installed from the Hub on the device. Find it in
    the App Catalog section and select to install it.

    In case of difficulties, see the [Troubleshooting] tips.

This completes the task.

Subsequent installations of your application can be made from Android Studio via
the Android Debug Bridge (adb), if you use the same signing configuration.  See
the [How to generate a signed Android package every build] instructions in this
document, if needed.

You can now proceed to the next task: [Obtain software development kit].

## Troubleshooting
In case **installation doesn't start** immediately, try any of the following:

-   Open the Hub application and select This Device, Managed Apps, and then your
    application.
-   Open the Hub application and select This Device, Sync device.
-   Terminate the Hub using the device task manager, then open Hub again.

There could be a number of **warnings about the trustworthiness** of the
application, if you used an ad hoc key store to sign the APK. These warnings are
generated by the device operating system because it doesn't recognise your ad
hoc certificate by default.

-   Accept the warnings to proceed.
-   The warnings shouldn't be displayed again after first installation. The
    device will recognize the certificate on subsequent installations, even if
    made via adb.

# Task: Obtain software development kit [Obtain software development kit]
Obtaining the Workspace ONE software development kit (SDK) is a platform
integration task for Android application developers. It applies to all levels of
platform integration.

## Download
The Workspace ONE mobile SDK for Android can be downloaded from VMware, for
example as follows.

1.  Open this page in a browser:  
    [https://code.vmware.com/web/sdk/Native/airwatch-android](https://code.vmware.com/web/sdk/Native/airwatch-android)

2.  Select the Download option.

    This will open the My Workspace ONE portal.
    
    As the warning on the page says: You must have a MyVMware username and
    password in able to sign in and complete your download.  
    (There is a special login option for VMware staff.)

3.  Log in to the portal.

4.  On the download page, select the required options.

    -   Select a platform: Android.
    -   Select an app version: 20.10 or whatever is the latest version.
    -   Filter by Console Version: All.

    Some resource downloads should now appear below the selection controls.

5.  Select to start the download.

    Select the Installs and Upgrades tab, then, under Software Downloads, select
    the VMware Workspace ONE SDK version link.

    This opens the End-User License Agreement page.

6.  Read the EULA, select the checkbox, and click Accept.

The SDK download will begin.

## Contents
Unpack the download and you will see that the SDK has the following principal
software components.

-   Client SDK library.
-   Framework library.
-   Networking library.
-   Privacy library.

The SDK download also includes the following.

-   Reference documentation for each of the above libraries.
-   Developer guides.
-   Third party libraries on which the above libraries depend.

See also the [Software Development Kit Download Structure Diagram].

## Software Development Kit Download Structure Diagram
The following diagram illustrates the directory structure of the SDK download.

![**Diagram 1:** Download structure of the SDK for Android](DownloadStructure.svg)

# Next Steps
This completes the preparation for integrating your Android application with the
Workspace ONE platform. You are now ready to start either of the following.

-   Client-level integration.
-   Framework-level integration.

See the Base Integration guide for instructions. The Base Integration Guide is
available

-   in Markdown format, in the repository that also holds the sample code:  
    [https://github.com/vmware-samples/...BaseIntegration.md](https://github.com/vmware-samples/workspace-ONE-SDK-integration-samples/blob/main/IntegrationGuideForAndroid/Guides/03BaseIntegration/WorkspaceONE_Android_BaseIntegration.md)

-   in Portable Document Format (PDF), on the VMware website:  
    [https://code.vmware.com/...BaseIntegration.pdf](https://code.vmware.com/docs/12356/WorkspaceONE_Android_BaseIntegration.pdf)

# Appendix: How to generate a signed Android package file once [How to generate a signed Android package file once]
You can generate a signed Android package file (APK) for your application by
following these instructions. These are provided here for convenience; for
definitive information, see the Android developer website.

1.  Open the project in Android Studio.

2.  In the menu, select Build, Generate Signed Bundle / APK.

    This opens the first step in the Generate Signed Bundle or APK dialog.

3.  In the dialog, select APK and then click Next.

    This opens the next step in the dialog.

4.  Select a key store path and enter the key store password.

    You can create a new key store and key ad hoc at this step. If you do then
    you can also set the key store password, and the individual key password
    here.

5.  Select a key, enter the key password, and then click Next.

    This opens the next step in the dialog.

6.  Make a note of the Destination Folder so that the APK file can be located
    after.

7.  Select a build variant, debug is fine.

8.  Select Signature Version V2 (Full APK Signature).

9.  Click Finish.

The processing runs and a notification will pop up in Android Studio. The
destination folder can be opened from a link in the notification. It can also be
opened from the Event Log panel, even after the notification has been dismissed.

The .apk file is the one to upload to the management console.

# Appendix: How to generate a signed Android package every build [How to generate a signed Android package every build]
You can configure Gradle to build a signed Android package file (APK) every time
you build the application by following these instructions. These are provided
here for convenience; for definitive information, see the Android developer
website.

1.  Create a key store file.

    You can create a key store file by following the
    [How to generate a signed Android package file once] instructions in this
    document.

    The details of the key and key store file will be needed for the next step.

2.  Create a script plugin for the key store.

    You can create a Gradle script plugin file that adds the signing
    configuration to an Android application build specification. The file could
    look like this:

        android {
            signingConfigs {
                debug {
                    storeFile file('/path/to/your/keystore')
                    storePassword 'password123'
                    keyPassword 'password456'
                    keyAlias = 'key0'
                }
            }
        }

    The name of the file could be like `keystore.gradle` for example.
    
    The location of the file should be outside the application directory, unless
    you want to place the passwords under revision control.

3.  Apply the plugin to the application build.

    In the application module build.gradle file, after the android block, insert
    an apply command, for example as follows.

        android {
            // Existing configuration such as ...
            compileSdkVersion 28
            defaultConfig {
                // ...
            }
            buildTypes {
                // ...
            }
        }

        // Following line is inserted to apply the signing configuration.
        apply from: file("/path/to/keystore.gradle")

Every time the application is built, it will now be signed.

# Appendix: How to verify that an Android package file is signed
You can verify that an APK file is signed, by using the apksigner tool. The
following notes are provided for convenience; for definitive information, see
the Android developer website.

The tool comes with Android Studio. The command line is like this:

    /path/to/Android/sdk/build-tools/version/apksigner verify --verbose /path/to/App-debug.apk

The top of the output should be like this:

    Verifies
    Verified using v1 scheme (JAR signing): true
    Verified using v2 scheme (APK Signature Scheme v2): true
    Number of signers: 1

After that, there could be a large number of warnings. Those can be ignored.

# Appendix: How to upload an Android application to the management console [How to upload an Android application to the management console]
You can upload an APK file to the Workspace ONE management console by following
these instructions. These are provided here for application developer
convenience and aren't intended to replace the system administrator user guides
for the Workspace ONE product.

For context of when these instructions would be followed, see the
[install your application via Workspace ONE] task.

1.  Open the Workspace ONE management console in a web browser and log in.

    This opens the dashboard.

2.  From the dashboard, navigate to: Apps & Books, Applications, Native.

    This opens a list of applications.

2.  Select: Add Application.

    This opens the Add Application dialog.

3.  Select the group of the end user that you are using for development.

4.  Click Upload, which opens the Add dialog.

5.  On the Add dialog: select Local File, then click Choose file.

    This opens a file chooser dialog.

6.  Locate and select your signed APK file, then click Save.

    The file will be uploaded and progress will be indicated on the screen.

    When the upload finishes, the Add dialog closes and you return to the Add
    Application dialog. The file name will have been filled in.

7.  On the Add Application dialog, click Continue.

    This opens the next step, which is the Edit Application dialog.

8.  Append your user name to the application name, if you like, and click Save &
    Assign.

    Appending your user name will make clear, to anybody with access to the
    console, that you are responsible for this application.

    After you click, the Update Assignment dialog will open.

9.  Add an assignment to the required group.

    In the Update Assignment dialog, click Add Assignment. On the dialog that
    appears, select the same group as before, then click Add. There is no need
    to add or enable any other items, like DLP, at this time.
    
    This returns you to the Update Assignment dialog. The assignment that you
    just added should now appear.

10.  Click Save And Publish.

    This opens the Preview Assigned Devices screen, which you can ignore.

11. Click Publish.

    This finalizes the addition and returns you to the application list.

The application that you uploaded can now be installed from Hub application.

See also the [Troubleshooting] tips elsewhere in this document.

# Appendix: How to run integrated applications on Huawei devices
Additional preparation of some Huawei mobile devices is required in order to run
applications that have integrated the Workspace ONE mobile software development
kit.

On some devices, an integrated application will crash when launched, if the
anchor app, either Workspace ONE Intelligent Hub or Workspace ONE, isn't already
running.

The crash can be prevented by setting up Secondary Launch Management on the
device. Proceed as follows.

1.  On the device, launch the **Tablet Manager** or **Phone Manager** app.
2.  Select the **Auto-Launch** option and **Secondary Launch Management**.
3.  Enable for Secondary Launch whichever anchor app is installed, either
    Workspace ONE Intelligent Hub or Workspace ONE.

This completes the additional preparation.

# Document Information
## Published Locations
This document is available

-   in Markdown format, in the repository that also holds the sample code:  
    [https://github.com/vmware-samples/...IntegrationPreparation.md](https://github.com/vmware-samples/workspace-ONE-SDK-integration-samples/blob/main/IntegrationGuideForAndroid/Guides/02Preparation/WorkspaceONE_Android_IntegrationPreparation.md)

-   in Portable Document Format (PDF), on the VMware website:  
    [https://code.vmware.com/...IntegrationPreparation.pdf](https://code.vmware.com/docs/12355/WorkspaceONE_Android_IntegrationPreparation.pdf)

## Revision History
|Date     |Revision                                    |
|---------|--------------------------------------------|
|03jul2020|First publication, for 20.4 SDK for Android.|
|31jul2020|Updated for 20.7 SDK for Android.           |
|31aug2020|Updated for 20.8 SDK for Android.           |
|03sep2020|Post-release update.                        |
|01oct2020|Updated for 20.9 SDK for Android.           |
|11oct2020|Post-release update.                        |
|03nov2020|Updated for 20.10 SDK for Android.          |
|06nov2020|Post-release update.                        |

## Legal
-   **VMware, Inc.** 3401 Hillview Avenue Palo Alto CA 94304 USA
    Tel 877-486-9273 Fax 650-427-5001 www.vmware.com
-   Copyright © 2020 VMware, Inc. All rights reserved.
-   This content is protected by U.S. and international copyright and
    intellectual property laws. VMware products are covered by one
    or more patents listed at
    [https://www.vmware.com/go/patents](https://www.vmware.com/go/patents).
    VMware is a registered trademark or trademark of VMware, Inc. and its
    subsidiaries in the United States and other jurisdictions. All other marks
    and names mentioned herein may be trademarks of their respective companies.
-   The Workspace ONE Software Development Kit integration samples are
    licensed under a two-clause BSD license.  
    SPDX-License-Identifier: BSD-2-Clause