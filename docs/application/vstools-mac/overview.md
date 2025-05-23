# Visual Studio for Mac Extension for Tizen

> [!NOTE]
> There is no further distribution plan for Visual Studio for Mac Extension for Tizen after Oct. 29, 2021 release (version 1.6).


Visual Studio for Mac Extension for Tizen is an extension that enables you to develop Tizen .NET applications easily using various Tizen project templates with Visual Studio for Mac.


## Prerequisites

To work with Visual Studio for Mac Extension for Tizen, your computer must have:

- At least 5.6 GB of available disk space
- macOS Catalina version 10.15, Big Sur version 11.04 (Community, Professional, and Enterprise)
- Visual Studio 2019 for Mac version 8.6 and higher (Community, Professional, and Enterprise)
- Java Development Kit (JDK)

  > [!NOTE]
  > To use Tizen Baseline SDK version earlier than version 3.7, you must install [Oracle Java Development Kit(JDK) 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) and [Java for OS X 2017-001](https://support.apple.com/kb/DL1572) together or [OpenJDK 12 and OpenJFX](../tizen-studio/setup/openjdk.md#install-openjdk-for-macos).

## Install Visual Studio for Mac Extension

To install Visual Studio for Mac Extension for Tizen:

1. In the Visual Studio Mac IDE menu, select **Visual Studio > Extensions**.

   ![Install extension](media/install-extension1.png)

2. In the **Extension Manager** dialog that appears, click **Gallery**.

	![Extension Manager](media/install-extension2.png)

3. To get the latest extensions, click **Refresh**.

	![Browse Extension](media/install-extension3.png)

4. After the extension list is refreshed, expand **IDE extensions**, select **Visual Studio for Mac Extension for Tizen**, and click **Install**.

	![Install Popup](media/install-extension4.png)
	![Install Popup1](media/install-extension5.png)

5. In the **VisualStudio** dialog that appears, click **Install**.

    ![Install Popup2](media/install-extension6.png)

   The extension is installed.

   > [!NOTE]
   > To complete the installation, restart the IDE.

   After successful installation, **Tizen** appears in the project wizard.

   ![Project Wizard](media/install-extension7.png)

## Install Tizen Baseline SDK

Baseline SDK contains Tizen-specific libraries and tools such as profiler, debugger, and so on.

After installing Visual Studio for Mac Extension for Tizen, you must set up Tizen Baseline SDK. You can either:

- [Install a new Tizen Baseline SDK](#install-a-new-tizen-baseline-sdk) if you have not already installed the SDK.
- [Configure an existing Tizen Baseline SDK](#configure-an-existing-tizen-baseline-sdk) if you want to use the installed SDK.

### Install a new Tizen Baseline SDK

1. In the Visual Studio Mac IDE menu, go to **Tools > Tizen > Tizen Package Manager**.
2. Select **Install new Tizen SDK**.

   ![Select new installation](media/howtoinstall-installwizard1.png)

3. Read the license document and click **I Agree**.

   ![Agree to license details](media/howtoinstall-installwizard2.png)

4. Enter the root directory path where you want to install Tizen Baseline SDK and click **Next**.

   ![Set the installation path](media/howtoinstall-installwizard3.png)

   Tizen SDK installer is downloaded and Baseline SDK is installed automatically.

   ![Installer download](media/howtoinstall-installwizard4.png)

5. In the **Package Manager** window that appears, select **Main SDK**.

6. Select **Tizen SDK tools** and click **install**. You can see the installation progress in the **Progress** tab.

   ![Tool installation](media/howtoinstall-installwizard6.png)

<a name="configure-an-existing-tizen-baseline-sdk"></a>
### Configure an existing Tizen Baseline SDK

You can also use Tizen Package Manager to configure Tizen Baseline SDK path and each tool path directly:

- To set up Tizen Baseline SDK path:

  1. In the Visual Studio Mac IDE menu, select **Tools > Tizen > Tizen Package Manager**.
  2. Select **Use installed Tizen SDK**.

     ![Baseline SDK Install](media/howtoinstall-installwizard7.png)

  3. Enter the root directory of your existing Tizen Baseline SDK installation and click **Ok**.

     ![Baseline SDK Install](media/howtoinstall-installwizard8.png)

     Tizen Baseline SDK is installed automatically.

     > [!NOTE]
     > If the installer gives a warning about your Tizen Studio version being too low, update Tizen Baseline SDK by using Tizen Package Manager after setting the tool path.

- To set up each tool path directly:

  1. In the Visual Studio Mac IDE menu, select **Project > Solution Options > Tizen > Tools**.
  2. Enter the root directory of your existing Tizen Studio installation in the **Tool Path(Tizen SDK)** field.

     ![Check the SDK tool path](media/howtoinstall-checktoolpath.png)

     The other tool paths are configured automatically.


## Troubleshoot

If you encounter any issue with the installation, verify whether Tizen Baseline SDK is installed correctly.

To verify that, go to **Project > Solution Options > Tizen > Tools** and verify the tool path.

![Check the SDK tool path](media/howtoinstall-checktoolpath.png)
