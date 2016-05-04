---
author: joshbax-msft
title: OPM - HDCP CSS DVD Test2
description: OPM - HDCP CSS DVD Test2
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 4a0e3959-f173-4b4f-8a4f-0dc33055d1dd
---

# OPM - HDCP CSS DVD Test2


These automated tests run PVP-OPM (Protected Video Path - Output Protection Management) commands. They test display drivers for PVP-OPM compatibility, and check for the availability of digital protection (HDCP) and analog protections (ACP and CGMSA).

There are three assertions for this test:

-   The display driver must support PVP-OPM driver interfaces.

-   The display driver must support CGMSA and APS.

-   The display driver must support HDCP.

For all of the assertions, the test goes through the PVP-OPM initialization protocol. If initialization fails, all of the assertions fail for premium SKUs (and skip for basic SKUs). Tests do not actually verify each protection schema, but do query the driver for the availability.

This topic applies to the following test jobs:

-   OPM - HDCP CSS DVD Test

-   OPM - HDCP CSS DVD Test (WoW64)

-   OPM - HDCP Test

-   OPM - HDCP Test (WoW64)

-   OPM - Protocol Test

-   OPM - Protocol Test (WoW64)

## Test details


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Associated requirements</strong></p></td>
<td><p>Device.Graphics.WDDM.DisplayRender.OutputProtection Device.Graphics.WDDM.DisplayRender.OutputProtection.Windows7 Device.Graphics.WDDM11.DisplayRender.Base</p>
<p>[See the device hardware requirements.](http://go.microsoft.com/fwlink/p/?linkid=254483)</p></td>
</tr>
<tr class="even">
<td><p><strong>Platforms</strong></p></td>
<td><p>Windows 7 (x64) Windows 7 (x86) Windows 8 (x64) Windows 8 (x86) Windows Server 2012 (x64) Windows Server 2008 R2 (x64) Windows 8.1 x64 Windows 8.1 x86 Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p><strong>Expected run time</strong></p></td>
<td><p>~10 minutes</p></td>
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


Before you run the test, complete the test setup as described in the test requirements: [Graphic Adapter or Chipset Testing Prerequisites](graphic-adapter-or-chipset-testing-prerequisites.md).

In addition:

-   If the graphics card supports a digital connector (DVI or HDMI), you must connect and enable an HDCP-enabled monitor.

-   If the graphics card supports an analog connector (component, composite, or S-Video), you must connect and enable the analog connector.

## Troubleshooting


For troubleshooting information, see [Troubleshooting Device.Graphics Testing](troubleshooting-devicegraphics-testing.md).

## More information


The following jobs validate the test assertions below:

-   OPM - HDCP CSS DVD Test

-   OPM - HDCP Test

-   OPM - Protocol Test

### Command syntax

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
<td><p><strong>ShellRunner.exe -x premium -c OPM_CSSDVD_HDCP_Test.pro -l &quot;[WTTRunWorkingDir]\s98wtt_u.dll&quot;</strong></p></td>
<td><p>Runs the OPM - HDCP CSS DVD test job.</p></td>
</tr>
<tr class="even">
<td><p><strong>ShellRunner.exe -x premium -c OPM_CSSDVD_HDCP_Test.pro -l &quot;[WTTRunWorkingDir]\s98wtt_u.dll&quot;</strong></p></td>
<td><p>Runs the OPM - HDCP CSS DVD Test (WoW64) test job.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ShellRunner.exe -x basic -c OPM_HDCP_Test.pro -l &quot;[WTTRunWorkingDir]\s98wtt_u.dll&quot;</strong></p></td>
<td><p>Runs the OPM - HDCP test job.</p></td>
</tr>
<tr class="even">
<td><p><strong>ShellRunner.exe -x basic -c OPM_HDCP_Test.pro -l &quot;[WTTRunWorkingDir]\s98wtt_u.dll&quot;</strong></p></td>
<td><p>Runs the OPM - HDCP Test (WoW64) test job.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ShellRunner.exe -x basic -c OPM_Protocol_Test.pro -l &quot;[WTTRunWorkingDir]\s98wtt_u.dll&quot;</strong></p></td>
<td><p>Runs the OPM - Protocol test job.</p></td>
</tr>
<tr class="even">
<td><p><strong>ShellRunner.exe -x basic -c OPM_Protocol_Test.pro -l &quot;[WTTRunWorkingDir]\s98wtt_u.dll&quot;</strong></p></td>
<td><p>Runs the OPM - Protocol Test (WoW64) test job.</p></td>
</tr>
</tbody>
</table>

 

 

**Note**  
For command line help for this test binary, type **/h**.

 

### File List

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>File</th>
<th>Location</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Configdisplay.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\tools\</p></td>
</tr>
<tr class="even">
<td><p>OPM_ACPandCGMSA_Test.pro</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\</p></td>
</tr>
<tr class="odd">
<td><p>OpmCompTest.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\</p></td>
</tr>
<tr class="even">
<td><p>S98wtt_u.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\</p></td>
</tr>
<tr class="odd">
<td><p>Shellrunner.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\</p></td>
</tr>
<tr class="even">
<td><p>TDRWatch.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\windowstest\graphics\</p></td>
</tr>
</tbody>
</table>

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20OPM%20-%20HDCP%20CSS%20DVD%20Test2%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



