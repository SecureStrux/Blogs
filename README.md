# Apply Configuration With Microsoft’s LGPO Utility
Microsoft’s Local Group Policy Object (LGPO) Utility is a standalone command-line executable that assists administrators in automating the management of a computer’s local security policy. The tool uses a combination of Group Policy Template (GptTmpl.inf) files, Registry Policy (registry.pol) files, and Audit Policy (audit.csv) files to apply desired configuration settings to endpoints. In this article, you will learn how to use Microsoft's LGPO utility to baseline the configuration of a Windows 10 system.

## Prerequisites
This article is meant to convey information that teaches you how to baseline the configuration of a Windows 10 system. If you’d like to follow along with any of the demonstrations, you will need:

* A Windows 10 system
* Administrator rights on the Windows 10 system

---
**NOTE**

The commands that are used in this article will apply configuration changes to the target computer. It is recommended that the commands within this areticle are run on a test system or a virtual machine. Please proceed with caution!

---

## Downloading Microsoft's LGPO Utility
The LGPO utility is part of Microsoft's Security Compliance Toolkit. To download LGPO:
1. Navigate to the [Microsoft Security Compliance Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=55319) download page
2. Click **Download**:<br/><img src="https://user-images.githubusercontent.com/86627856/190912770-f5758cef-d046-49ec-97db-dd00512ada5c.png" width=50% height=50%>
3. Select **LGPO.zip** and then click **Next**:<br/><img src="https://user-images.githubusercontent.com/86627856/190913424-cae3a16d-b6ed-4bc8-bd9f-4fe3bd93139a.png" width=50% height=50%>
4. Navigate to your system's default download location and confirm that the download completed successfully.
