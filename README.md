# Apply Configuration With Microsoft’s LGPO Utility
Microsoft’s Local Group Policy Object (LGPO) Utility is a standalone command-line executable that assists administrators in automating the management of a computer’s local security policy. The tool uses a combination of Group Policy Template (GptTmpl.inf) files, Registry Policy (registry.pol) files, and Audit Policy (audit.csv) files to apply desired configuration settings to endpoints. In this article, you will learn how to use Microsoft's LGPO utility to baseline the configuration of a Windows 10 system.

## Prerequisites
This article is meant to convey information that teaches you how to baseline the configuration of a Windows 10 system. If you’d like to follow along with any of the demonstrations, you will need:

* A Windows 10 system
* Administrator rights on the Windows 10 system
* The latest version of Microsoft's LGPO utility

---
**NOTE**

The commands that are used in this article will apply configuration changes to the target computer. It is recommended that the commands within this areticle are run on a test system or a virtual machine. Please proceed with caution!

---

## About Microsoft's LGPO Utility
LGPO.exe functions as a standalone executable program that can be run directly from the command-line. It does not install additional software on your system to perform its tasks. 

1. Export local policy to a backup
2. Import and apply policy settings
3. Parse a registry.pol file to LGPO text format
4. Build a registry.pol file from LGPO text

---
**NOTE**

Additional information on how to use the LGPO Utility can be found within the LGPO.pdf file that comes embedded within the .zip download.

---

## Downloading Microsoft's LGPO Utility
The LGPO utility is part of Microsoft's Security Compliance Toolkit. To download LGPO:
1. Navigate to the [Microsoft Security Compliance Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=55319) download page
2. Click **Download**:<br/><img src="https://user-images.githubusercontent.com/86627856/190912770-f5758cef-d046-49ec-97db-dd00512ada5c.png" width=50% height=50%>
3. Select **LGPO.zip** and then click **Next**:<br/><img src="https://user-images.githubusercontent.com/86627856/190913424-cae3a16d-b6ed-4bc8-bd9f-4fe3bd93139a.png" width=50% height=50%>
4. Navigate to your system's default download location and confirm that the download completed successfully.
5. Extract the contents of the **LGPO.zip** archive:<br/><img src="https://user-images.githubusercontent.com/86627856/190913990-ba59e29b-b2a2-4db2-9ab1-25a00cd62b75.png" width=50% height=50%>

## Exporting Local Policy to a Backup with LGPO
Before applying a new policy, it is best practice to create a backup of your system’s current configuration. LGPO enables this functionality with the `/b` switch:
1. Navigate to the directory that contains the LGPO executable file (LGPO.exe). The LGPO.exe file used within this article is stored within **C:\LGPO**:
    ```PowerShell
    #Change directory location to C:\LGPO.
    cd C:\LGPO
    ```
2. Backup the system's current configuration using LGPO's `/b` switch. The following command will create and store a configuration backup within **C:\LGPO**:
    ```PowerShell
    #Backup the system's current configuration to C:\LGPO using LGPO's /b switch.
    C:\LGPO\LGPO.exe /b C:\LGPO
    ```
3. 
