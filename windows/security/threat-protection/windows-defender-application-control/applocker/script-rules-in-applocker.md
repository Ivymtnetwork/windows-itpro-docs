---
title: Script rules in AppLocker (Windows)
description: This topic describes the file formats and available default rules for the script rule collection.
ms.assetid: fee24ca4-935a-4c5e-8a92-8cf1d134d35f
ms.reviewer: 
ms.author: macapara
ms.prod: m365-security
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
author: mjcaparas
manager: dansimp
audience: ITPro
ms.collection: M365-security-compliance
ms.topic: conceptual
ms.date: 09/21/2017
ms.technology: mde
---

# Script rules in AppLocker

**Applies to**

- Windows 10
- Windows 11
- Windows Server 2016 and above

>[!NOTE]
>Some capabilities of Windows Defender Application Control are only available on specific Windows versions. Learn more about the [Defender App Guard feature availability](/windows/security/threat-protection/windows-defender-application-control/feature-availability).

This topic describes the file formats and available default rules for the script rule collection.

AppLocker defines script rules to include only the following file formats:
-   .ps1
-   .bat
-   .cmd
-   .vbs
-   .js

The following table lists the default rules that are available for the script rule collection.

| Purpose | Name | User | Rule condition type |
| - | - | - | - |
| Allows members of the local Administrators group to run all scripts| (Default Rule) All scripts| BUILTIN\Administrators | Path: *|
| Allow all users to run scripts in the Windows folder| (Default Rule) All scripts located in the Windows folder| Everyone | Path: %windir%\*| 
| Allow all users to run scripts in the Program Files folder| (Default Rule) All scripts located in the Program Files folder|Everyone | Path: %programfiles%\*| 
 
## Related topics

- [Understanding AppLocker default rules](understanding-applocker-default-rules.md)
