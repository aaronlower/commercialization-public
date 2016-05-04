---
author: joshbax-msft
title: Mouse or other Pointing Device Testing Prerequisites
description: Mouse or other Pointing Device Testing Prerequisites
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 81b1f992-e95c-4b94-89f7-27529033d39f
---

# Mouse or other Pointing Device Testing Prerequisites


This section describes the tasks that you must complete before you test a mouse or similar pointing device by using the Windows Hardware Certification Kit (Windows HCK):

-   [Review the hardware requirements](#bkmk-hck-mouse-hr).

-   [Review the software requirements](#bkmk-hck-mouse-sr).

-   [Configure the test computer](#bkmk-hck-mouse-tc).

## <a href="" id="bkmk-hck-mouse-hr"></a>Hardware requirements


The following hardware is required for testing a mouse or pointing device. You might need additional hardware if the test device offers other features. To determine whether additional hardware requirements apply, see the test description for each test displayed for the device in Windows HCK Studio.

-   One test computer. The test computer must meet the Windows HCK prerequisites. For more information, see [Windows HCK Prerequisites](windows-hck-prerequisites.md).

-   One test mouse or similar pointing device.

-   One USB 2.0 hub that has a logo.

## <a href="" id="bkmk-hck-mouse-sr"></a>Software requirements


The following software is required for testing a mouse or similar pointing device:

-   The drivers for the test device.

-   The latest Windows HCK filters or updates.

## <a href="" id="bkmk-hck-mouse-tc"></a>Test computer configuration


To configure the test computer for your test device, follow these steps:

1.  Install the appropriate Windows operating system on the test computer, and then configure the computer for your test network. The test network is the network that contains the Windows HCK Studio and Windows HCK Controller.

2.  Attach a USB 2.0 hub to the test computer.

3.  If the mouse or pointing device supports USB, attach the device to the test computer. Verify that the device is plugged into the external USB 2.0 high-speed hub that is connected to the test computer. To test a mouse that supports Bluetooth or wireless connections, connect the associated base station to the USB 2.0 hub

    **Note**  
    Do not connect the keyboard or wireless base station directly to the root hub of a USB 2.0 controller.

     

4.  If you have to install the manufacturer-supplied device driver on the test computer, do this now.

5.  Make sure that the mouse or pointing device functions correctly on the test computer.

6.  Install the Windows HCK client application on the test computer.

7.  Use Windows HCK Studio to create a machine pool, and then move the test computer to that pool.

Make sure that the test computer is in the ready state before you begin your testing. If a test requires parameters to be set before it is run, a dialog box will be displayed for that test. Review the specific test topic for more information.

Some Windows HCK tests require user intervention. When running tests for a submission, it is a best practice to run the automated tests in a block separately from manual tests. This prevents a manual test from interrupting completion of an automated test.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20Mouse%20or%20other%20Pointing%20Device%20Testing%20Prerequisites%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



