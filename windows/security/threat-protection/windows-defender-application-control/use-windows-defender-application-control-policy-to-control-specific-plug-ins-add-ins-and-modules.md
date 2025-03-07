---
title: Use a Windows Defender Application Control policy to control specific plug-ins, add-ins, and modules (Windows)
description: WDAC policies can be used not only to control applications, but also to control whether specific plug-ins, add-ins, and modules can run from specific apps.
keywords: security, malware
ms.assetid: 8d6e0474-c475-411b-b095-1c61adb2bdbb
manager: dansimp
ms.author: dansimp
ms.prod: m365-security
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.localizationpriority: medium
audience: ITPro
ms.collection: M365-security-compliance
author: jsuther1974
ms.reviewer: isbrahm
ms.date: 08/12/2021
ms.technology: mde
---

# Use a Windows Defender Application Control policy to control specific plug-ins, add-ins, and modules 

**Applies to:**

- Windows 10
- Windows 11
- Windows Server 2016 and above

> [!NOTE]
> Some capabilities of Windows Defender Application Control are only available on specific Windows versions. Learn more about the [Defender App Guard feature availability](feature-availability.md).

As of Windows 10, version 1703, you can use WDAC policies not only to control applications, but also to control whether specific plug-ins, add-ins, and modules can run from specific apps (such as a line-of-business application or a browser):

| Approach (as of Windows 10, version 1703) | Guideline |
|---|---|
| You can work from a list of plug-ins, add-ins, or modules that you want only a specific application to be able to run. Other applications would be blocked from running them. | Use `New-CIPolicyRule` with the `-AppID` option. |
| In addition, you can work  from a list of plug-ins, add-ins, or modules that you want to block in a specific application. Other applications would be allowed to run them. | Use `New-CIPolicyRule` with the `-AppID` and `-Deny` options. |

To work with these options, the typical method is to create a policy that only affects plug-ins, add-ins, and modules, then merge it into your 'master' policy (merging is described in the next section).

For example, to create a WDAC policy allowing **addin1.dll** and **addin2.dll** to run in **ERP1.exe**, your organization's enterprise resource planning (ERP) application, run the following commands. Note that in the second command, **+=** is used to add a second rule to the **$rule** variable:

```powershell
$rule = New-CIPolicyRule -DriverFilePath '.\temp\addin1.dll' -Level FileName -AppID '.\ERP1.exe'
$rule += New-CIPolicyRule -DriverFilePath '.\temp\addin2.dll' -Level FileName -AppID '.\ERP2.exe'
New-CIPolicy -Rules $rule -FilePath ".\AllowERPAddins.xml" -UserPEs
```

As another example, to create a WDAC policy that blocks **addin3.dll** from running in Microsoft Word, run the following command. You must include the `-Deny` option to block the specified add-ins in the specified application:

```powershell
$rule = New-CIPolicyRule -DriverFilePath '.\temp\addin3.dll' -Level FileName -Deny -AppID '.\winword.exe'
New-CIPolicy -Rules $rule -FilePath ".\BlockAddins.xml" -UserPEs
```
