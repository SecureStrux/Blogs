# Apply Configuration With Microsoft’s LGPO Utility
Microsoft’s Local Group Policy Object (LGPO) utility is a standalone command-line executable that assists administrators in automating the management of a computer’s local security policy. The tool uses a combination of Group Policy Template (GptTmpl.inf) files, Registry Policy (registry.pol) files, and Audit Policy (audit.csv) files to apply desired configuration settings to targeted endpoints. In this article you will learn how to use Microsoft's LGPO utility to baseline the configuration of a Windows 10 system using DISA's Group Policy Objects (GPO).

## Prerequisites
This article is meant to convey information that teaches you how to baseline the configuration of a Windows 10 system using DISA's Group Policy Objects (GPO). If you’d like to follow along with any of the demonstrations, you will need:

* A Windows 10 system.
* Administrator rights on the Windows 10 system.

---
**PROCEED WITH CAUTION!**

The commands that are used in this article will apply configuration changes to the target computer. It is recommended that the commands within this areticle are run on a test system or a virtual machine. The examples provided throughout this tutorial were generated using [Windows Sandbox](https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-sandbox/windows-sandbox-overview)

---

## About Microsoft's LGPO Utility
LGPO.exe functions as a standalone executable program that can be run directly from the command-line. LGPO.exe does not install additional software on your system to perform its tasks. LGPO.exe has four (4) core modes:
1. Export local policy to a backup.
2. Import and apply policy settings.
3. Parse a registry.pol file to LGPO text format.
4. Build a registry.pol file from LGPO text.

---
**NOTE**

Additional information on how to use the LGPO Utility can be found within the LGPO.pdf file that comes embedded within the .zip download.

---

## Downloading Microsoft's LGPO Utility
The LGPO utility is part of Microsoft's Security Compliance Toolkit. To download LGPO:
1. Navigate to the [Microsoft Security Compliance Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=55319) download page.
2. Click **Download**:<br/><img src="https://user-images.githubusercontent.com/86627856/190912770-f5758cef-d046-49ec-97db-dd00512ada5c.png" width=50% height=50%>
3. Select **LGPO.zip** and then click **Next**:<br/><img src="https://user-images.githubusercontent.com/86627856/190913424-cae3a16d-b6ed-4bc8-bd9f-4fe3bd93139a.png" width=50% height=50%>
4. Extract the contents of the **LGPO.zip** archive:<br/><img src="https://user-images.githubusercontent.com/86627856/190913990-ba59e29b-b2a2-4db2-9ab1-25a00cd62b75.png" width=50% height=50%>

## Downloading DISA's GPO Bundle
DISA packages preconfigure GPO templates to assist with the STIG implementation process. To download DISA's GPO bundle:
1. Navigate to the [DoD Cyber Exchange's Group Policy Objects](https://public.cyber.mil/stigs/gpo/) download page.
2. Click the GPO title under **GPO Downloads**. In the following screenshot you will see that the GPO title is **Group Policy Objects (GPOs) - July 2022**:<br/><img src="https://user-images.githubusercontent.com/86627856/191016877-154ad6d9-b8a5-44e1-9069-715f28bf0a68.png" width=50% height=50%>
3. Be patient as the GPO bundle download completes.
4. Extract the contents of the DISA GPO .zip archive:<br/><img src="https://user-images.githubusercontent.com/86627856/191019049-4915ca70-45ac-4946-867a-5b0ad2930597.png" width=50% height=50%>

## Preparing Your System
If you want to follow along, please use the following steps to mirror the setup of the system that was used to create this article:
1. Open a PowerShell session as an Administrator.
2. Use the following command to create a new directory named **LGPO**:
    ```PowerShell
    #Create the C:\LGPO directory.
    mkdir C:\LGPO
    ```
3. Copy the **LGPO.exe** executable file from your **Downloads** directory to **C:\LGPO**
4. Copy the **DoD Windows 10 v[x]r[x]** from the unzipped DISA GPO archive to **C:\LGPO**<br/><img src="https://user-images.githubusercontent.com/86627856/191022647-2191c32c-f09c-456a-b2a9-8cc9fd5f2c8f.png" width=50% height=50%>
5. Change your directory location to **C:\LGPO** using the `cd` command:
    ```PowerShell
    #Change directory location to C:\LGPO.
    cd C:\LGPO
    ```
6. Issue the `dir` command to list the contents of **C:\LGPO** and confirm that **LGPO.exe** is listed:<br/><img src="https://user-images.githubusercontent.com/86627856/191020711-6c59adca-cd18-41fd-a4c0-7844a76be9f9.png" width=50% height=50%>

Nice job! Your system is ready to go! In the next section you will use LGPO to backup your systems current configuration.

## Exporting Local Policy to a Backup with LGPO
Before applying a new policy, it is best practice to create a backup of your system’s current configuration. LGPO enables this functionality with the `/b` switch:
1. Open a PowerShell session as an Administrator.
2. Backup your system's current configuration using LGPO's `/b` switch. The following command will create and store a configuration backup within **C:\LGPO**:
    ```PowerShell
    #Backup the system's current configuration to C:\LGPO using LGPO's /b switch.
    C:\LGPO\LGPO.exe /b C:\LGPO
    ```
3. Confirm that the command completes without error:<br/><img src="https://user-images.githubusercontent.com/86627856/190925937-9a995aed-b908-4704-8714-e470490dc8a1.png" width=50% height=50%>

Great work! The configuration backup process is now complete! In the next section you will baseline the configuration of your Windows 10 system using DISA's Group Policy Objects (GPO).

## Apply Local Policy using LGPO
Now that you've obtained a backup of your system's local policy, it is time to apply the new configuration. You can import settings from one or more Group Policy Objects (GPO) using LGPO's `/g` switch:

---
**NOTE**

DISA's Windows 10 GPO contains place holders that require organization-specific values for the following [User Rights Assignments](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/user-rights-assignment):
1. **Deny access to this computer from the network**: ADD YOUR ENTERPRISE ADMINS,ADD YOUR DOMAIN ADMINS
2. **Deny log on as a batch job**: ADD YOUR ENTERPRISE ADMINS,ADD YOUR DOMAIN ADMINS
3. **Deny log on as a service**: ADD YOUR ENTERPRISE ADMINS,ADD YOUR DOMAIN ADMINS
4. **Deny log on locally**: ADD YOUR ENTERPRISE ADMINS,ADD YOUR DOMAIN ADMINS
5. **Deny log on through Remote Desktop Services**: ADD YOUR ENTERPRISE ADMINS,ADD YOUR DOMAIN ADMINS

Insert your specific values prior to, or after, execution of the commands identified below.

---

1. Open a PowerShell session as an Administrator.
2. Apply the **DoD Windows 10 v[x]r[x]** using LGPO's `/g` switch:
    ```PowerShell
    #Apply the DoD Windows 10 v[x]r[x] configuration using LGPO's /g switch.
    #NOTE: You may need to modify the version and revision (v[x]r[x]) numbers. At the time of this writing, the DoD Windows 10 GPO is v2r4.
    C:\LGPO\LGPO.exe /g "C:\LGPO\DoD Windows 10 v2r4"
    ```
3. Confirm that the command completes without error:
