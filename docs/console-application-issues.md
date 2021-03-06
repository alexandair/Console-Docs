---
title: Console Application Issues
description: The 8-bit console functions use the OEM code page.
author: bitcrazed
ms.author: richturn
ms.topic: article
ms.prod: console
keywords: console, character mode applications, command line applications, terminal applications, console api
---

# Console Application Issues


The 8-bit console functions use the OEM code page. All other functions use the ANSI code page by default. This means that strings returned by the console functions may not be processed correctly by the other functions and vice versa. For example, if **FindFirstFileA** returns a string that contains certain extended ANSI characters, **WriteConsoleA** will not display the string properly.

The best long-term solution for a console application is to use Unicode. Barring that solution, a console application should use the [**SetFileApisToOEM**](https://msdn.microsoft.com/library/windows/desktop/aa365534) function. That function changes relevant file functions so that they produce OEM character set strings rather than ANSI character set strings.

The following are file functions:

|                                                     |                                                       |                                                     |
|-----------------------------------------------------|-------------------------------------------------------|-----------------------------------------------------|
| [**CopyFile**](https://msdn.microsoft.com/library/windows/desktop/aa363851)                       | [**GetFileAttributes**](https://msdn.microsoft.com/library/windows/desktop/aa364944)       | [**LoadLibrary**](https://msdn.microsoft.com/library/windows/desktop/ms684175)                 |
| [**CreateDirectory**](https://msdn.microsoft.com/library/windows/desktop/aa363855)         | [**GetFullPathName**](https://msdn.microsoft.com/library/windows/desktop/aa364963)           | [**LoadLibraryEx**](https://msdn.microsoft.com/library/windows/desktop/ms684179)             |
| [**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)                   | [**GetModuleFileName**](https://msdn.microsoft.com/library/windows/desktop/ms683197)       | [**MoveFile**](https://msdn.microsoft.com/library/windows/desktop/aa365239)                       |
| [**CreateProcess**](https://msdn.microsoft.com/library/windows/desktop/ms682425)             | [**GetModuleHandle**](https://msdn.microsoft.com/library/windows/desktop/ms683199)           | [**MoveFileEx**](https://msdn.microsoft.com/library/windows/desktop/aa365240)                   |
| [**DeleteFile**](https://msdn.microsoft.com/library/windows/desktop/aa363915)                   | [**GetSystemDirectory**](https://msdn.microsoft.com/library/windows/desktop/ms724373)     | [**OpenFile**](https://msdn.microsoft.com/library/windows/desktop/aa365430)                       |
| [**FindFirstFile**](https://msdn.microsoft.com/library/windows/desktop/aa364418)             | [**GetTempFileName**](https://msdn.microsoft.com/library/windows/desktop/aa364991)           | [**RemoveDirectory**](https://msdn.microsoft.com/library/windows/desktop/aa365488)         |
| [**FindNextFile**](https://msdn.microsoft.com/library/windows/desktop/aa364428)               | [**GetTempPath**](https://msdn.microsoft.com/library/windows/desktop/aa364992)                   | [**SearchPath**](https://msdn.microsoft.com/library/windows/desktop/aa365527)                   |
| [**GetCurrentDirectory**](https://msdn.microsoft.com/library/windows/desktop/aa364934) | [**GetVolumeInformation**](https://msdn.microsoft.com/library/windows/desktop/aa364993) | [**SetCurrentDirectory**](https://msdn.microsoft.com/library/windows/desktop/aa365530) |
| [**GetDiskFreeSpace**](https://msdn.microsoft.com/library/windows/desktop/aa364935)       | [**GetWindowsDirectory**](https://msdn.microsoft.com/library/windows/desktop/ms724454)   | [**SetFileAttributes**](https://msdn.microsoft.com/library/windows/desktop/aa365535)     |
| [**GetDriveType**](https://msdn.microsoft.com/library/windows/desktop/aa364939)               |                                                       |                                                     |
||
||
||
||
||
||
||

 

When dealing with command lines, a console application should obtain the command line in Unicode form and convert it to OEM form, using the relevant character-to-OEM functions. Note, also, that *argv* uses the ANSI character set.

 

 




