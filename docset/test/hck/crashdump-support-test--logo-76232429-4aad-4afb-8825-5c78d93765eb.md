---
author: joshbax-msft
title: Crashdump Support Test (LOGO)
description: Crashdump Support Test (LOGO)
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: fd6e3547-1cfe-49fb-8f34-e46925c2ae63
---

# Crashdump Support Test (LOGO)


This test verifies that the storage miniport driver on Windows supports the creation of a memory dump file after a system stop error occurs.

## Test details


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Associated requirements</strong></p></td>
<td><p>Device.Storage.Controller.Boot.BasicFunction System.Fundamentals.StorageAndBoot.BootPerformance</p>
<p>[See the system hardware requirements.](http://go.microsoft.com/fwlink/p/?linkid=254482)</p></td>
</tr>
<tr class="even">
<td><p><strong>Platforms</strong></p></td>
<td><p>Windows 7 (x64) Windows 7 (x86) Windows RT (ARM-based) Windows 8 (x64) Windows 8 (x86) Windows Server 2012 (x64) Windows Server 2008 R2 (x64) Windows Server 2008 x64 Windows Server 2008 x86Windows RT 8.1Windows 8.1 x64Windows 8.1 x86Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p><strong>Expected run time</strong></p></td>
<td><p>~45 minutes</p></td>
</tr>
<tr class="even">
<td><p><strong>Categories</strong></p></td>
<td><p>Certification Functional</p></td>
</tr>
<tr class="odd">
<td><p><strong>Type</strong></p></td>
<td><p>Automated</p></td>
</tr>
</tbody>
</table>

 

## Running the test


Before you run the test, complete the test setup that is described in the test requirements for the kind of storage controller that you are testing. For more info, see [Storage Adapter or Controller Testing Overview](storage-adapter-or-controller-testing-overview.md).

This test requires additional software and hardware:

-   Device to be tested

-   Hard drive with a minimum of 20 GB available on partition **C:**.

Before you run the test, you must also complete the following prerequisites:

-   If your test system has an Internet connection, no action needs to be taken.

    If your test system does not have an Internet connection, create a folder named **C:\\Symbols** and download and install Windows operating system symbols. To do this, follow these steps:

    **Note**  
    Symbols are needed to analyze the dump file. Failure to install symbols is the most common test setup problem that causes this test to fail. The version of the symbols must match the version of operating system that is installed on the test machine. Therefore, it must be downloaded external to the kit.

     

    1.  On a machine that has an Internet connection, download the Windows Symbols packages. For more information, see [Download Windows Symbol Packages](http://msdn.microsoft.com/windows/hardware/gg463028.aspx).

    2.  Copy the symbol files to the test machine to the **C:\\Symbols** folder. Because the symbols can be large, you only need to copy **ntkrnlmp.pdb** (for x64 or ARM) or **ntkrpamp.pdb** (for x86).

## Troubleshooting


For troubleshooting information, see [Troubleshooting Device.Storage Testing](troubleshooting-devicestorage-testing.md).

-   **The test logs error message "Failed to load the correct symbols"**

    Upon reboot, the test examines the dump file for correctness. The test does this, just as a developer would, by using the kernel debugger kd (see [Download and Install Debugging Tools for Windows](http://go.microsoft.com/fwlink/p/?linkid=103787)). To analyze a dump file, the debugger needs access to symbols (see [Symbol Files](http://go.microsoft.com/fwlink/p/?linkid=231439)). This is a dictionary for the dump. They allow the debugger to analyze the contents of memory (or a crashdump file) into individual modules (executables, libraries, drivers, etc), functions within those modules, and data structures. As a general rule, if you cannot examine the dump file by using the kernel debugger, the test cannot pass.

    For the test to work properly, it needs to provide the debugger with symbols. When it does not have proper symbols, it will log warnings during the log failures during the first analysis phase of testing. The current mechanism for doing this is to download public symbol packages (see [Download Windows Symbol Packages](http://go.microsoft.com/fwlink/p/?linkid=316881)) and install them on the test machine before running the test. When symbols are not installed or do not match the operating system under test, the following message can appear in the test log:

    -   (x) Failed to load the correct symbols.

    -   (i) Please refer to WDK documentation on how to install operating system symbols.

    -   (i) Your symbols might also be out of date, please update symbols by using the [Microsoft Symbol Server](http://go.microsoft.com/fwlink/p/?linkid=316876).

    This message does not actually cause the test to fail because in some cases, the dump can still be analyzed with partially matching symbols. If the test continues and more test cases fail with messages such as *Error retrieving addresses of ...* or *Unable to get...,* it means that the debugger cannot analyze the dump because of missing symbols. One way to work around a symbol is to supplement the locally installed symbol packaged with symbols that are cached from an Internet symbol server. Follow these steps to cache the symbols locally:

    1.  Ensure that you have already created a crashdump. The easiest way to do this is to run the test once and let it fail.

    2.  Ensure that you have the debugging tools installed. Again the easiest way to do this is to run the test once. It will install the tools to **C:\\Debuggers**.

    3.  Open an elevated command prompt.

    4.  Type the following command **c:\\Debuggers\\kd -z c:\\Windows\\MEMORY.DMP -y SRV\*C:\\Symbols\*http://msdl.microsoft.com/download/symbols**

    5.  This loads the dump in the kernel debugger by using the remote symbol store at Microsoft and the local directory **C:\\Symbols** as the downstream store to cache the symbols.

    6.  Make sure that symbols can be found for operating system files such as **NTOSKRNL** and **NTDLL**. These files are necessary to analyze the dump. It is OK if errors appear loading symbols for other modules, such as third-party drivers.

    7.  You should now have a prompt **0: kd&gt;**. At this prompt, type the command **.reload /f**. This command forces the debugger to load and cache all symbols for modules loaded in the dump.

    8.  To exit the debugger, press **Ctrl-B** and then press **Enter**.

-   **The test logs error message "Paging file size is too small for full dump purposes"**

    In the case of a crash, there is no certainty of what parts of the operating system will still be functional. The network or file system drivers might have caused the crash; for example, preventing access to file system structures to create a dump file, or network to store the file remotely. The operating system handles this by using a file that it already knows exists (the pagefile) and writes directly to that file's logical block extents on disk. The dump process writes the contents of physical memory into the pagefile on the system disk (usually **c:\\pagefile.sys**). The pagefile must be large enough to contain the dump. The largest dump is a complete dump, which requires the size of physical memory (for example, 4096) plus one extra megabyte to contain the header information. The test requires that the user configure the page file to an appropriate size before execution. If the page file size is insufficient, the test will log the following error during the initialization phase:

    -   (i) Verifying paging file size.

    -   (x) Paging file size is too small for full dump purposes.

    -   (i) Paging file size: 330989568

    -   (i) Physical memory size: 1073094656

    -   (i) Please configure minimum paging file size to physical RAM size + 1MB.

-   **I see the system stop error (blue screen), but the bugcheck code is not E2**

    After some basic settings validation, the test will install a driver that is used to crash the system and reboot the system. After the reboot, the test changes the crash control settings (for full memory dump), deletes any old dump files, and crashes the system. At the point of the crash, the system will display a bugcheck screen (blue screen) with details of the nature of the crash. The type of bugcheck should be **MANUALLY\_INITIATED\_CRASH (e2)**. If anything else appears here, it means that a second bugcheck occurred during the process of writing the dump file. This should be investigated by connecting a kernel debugger to the test client and debugging the storage adapter driver.

-   **The test logs error message "Dump file is being used by another process. HRESULT: 0x80070020"**

    After the dump file has been written, the test machine should automatically reboot. Upon boot after a crash, the operating system will detect the presence of dump information in the page file and begin the process of writing a dump. This process occurs asynchronously while the machine is booting and even after the user has logged in. During this process, you can view progress by checking the size of the dump file (**C:\\windows\\memory.dmp**) or viewing the process in task manager (**werfault.exe**). The test will often be running at the same time as this process, trying to access the same dump file. If this occurs, the following messages will appear in the log:

    -   (i) Connecting to DumpFile: **C:\\Windows\\MEMORY.DMP**

    -   (i) Dump file is being used by another process. HRESULT: 0x80070020

    -   (i) Usually memory.dmp is still being written due to large RAM, retry after 5 minutes.

    The test should then retry accessing the file. If the error message code is different, or if it changes (for example, 0x80070002 : ERROR\_FILE\_NOT\_FOUND), then it means that the file could not be written to disk. The first place to check for valuable debug information is the system event log. To view the event log click **Start**, click **Run**, and then type **Compmgmt.msc**. In the computer management window, select **Computer Management\\System Tools\\Event Viewer\\System**. Browse through the list of events for an event that has the source **BugCheck**. The most common cause for a missing dump file is insufficient free space on the disk. The registry key **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\CrashControl\\MachineCrash** contains information about the last crash (before a reboot), including the partial dump file if one was created. This can be useful when trying to debug other missing dump issues.

## More information


Crashdump is the mechanism in which the operating system calls the storage adapter driver to write the contents of the memory to a dump file after a system stop error. Due to the nature of a system stop error, the operating system cannot make any assumptions about the stability of the system. Therefore, very few system services are available to the storage drivers. The Crashdump Support Test verifies that the storage adapter driver can still operate under these constrained environments and perform the I/O to write to the dump successfully.

The Windows operating system allows three different types of memory dump files to be generated:

-   Full

-   Kernel

-   Mini

The test will test all three dump file types. For further more about these dump file types, see [Kernel-Mode Dump Files](http://go.microsoft.com/fwlink/p/?linkid=308945).

The test will complete the following sequence of operations:

1.  Install Debugging Tools for Windows to the **%SystemDrive%\\Debuggers** directory and initialize the system.

2.  Install test driver to simulate crash.

3.  Set the pagefile size.

4.  Simulate system stop errors (bluescreen) with bugcheck code 0x000000E2.

5.  Reboot the system and automatically restart the test.

6.  Examine the previous crash by analyzing the memory dump file through the kernel debugger, and verify that the dump has been written correctly.

7.  Repeat steps 4 - 6 for each dump file type.

### Parameters

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SymbolsDirectory</p></td>
<td><p>Directory where the symbols are already installed.</p></td>
</tr>
<tr class="even">
<td><p>DebuggerDirectory</p></td>
<td><p>Directory in which to install the debuggers.</p></td>
</tr>
<tr class="odd">
<td><p>PagefileSize</p></td>
<td><p>The size of the paging file (in MB). This supports mem+N format.</p></td>
</tr>
</tbody>
</table>

 

### Command syntax

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Command</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Crashdumptest.exe -c</strong></p></td>
<td><p>Clear any past failures.</p></td>
</tr>
<tr class="even">
<td><p><strong>crashdumptest.exe -dtm -y [SymbolsDirectory] -ypass</strong></p></td>
<td><p>Initialize the test.</p></td>
</tr>
<tr class="odd">
<td><p><strong>crashdumptest.exe -autorun -y [SymbolsDirectory] -dtm&quot;</strong></p></td>
<td><p>Runs the test.</p></td>
</tr>
</tbody>
</table>

 

### File list

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Command option</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Crashdumptest.exe</p></td>
<td><p><em>[TestBinRoot]</em>\nttest\driverstest\storage\wdk\</p></td>
</tr>
<tr class="even">
<td><p>BugCheck.sys</p></td>
<td><p><em>[TestBinRoot]</em>\nttest\driverstest\storage\wdk\</p></td>
</tr>
</tbody>
</table>

 

 

 





