---
author: joshbax-msft
title: TargetFamliy.TargetsAreValidInSameTargetFamily(StringBuilder) Method
description: TargetFamliy.TargetsAreValidInSameTargetFamily(StringBuilder) Method
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: e3fe3e3b-4f95-4c27-9ae9-405e9949944c
---

# TargetFamliy.TargetsAreValidInSameTargetFamily(StringBuilder) Method


This method checks to see if the two TargetData objects can be members of the same target family.

**Namespace:** Microsoft.Windows.Kits.Hardware.ObjectModel **Assembly:** Microsoft.Windows.Kits.Hardware.ObjectModel (in Microsoft.Windows.Kits.Hardware.ObjectModel)

## Syntax


**Visual Basic**`Public Shared Function TargetsAreValidInSameTargetFamily(ByVal firstTarget As TargetData, ByVal secondTarget As TargetData, ByVal manager As ProjectManager, ByVal builder As StringBuilder) As Boolean`

**C#**`public static bool TargetsAreValidInSameTargetFamily(TargetData firstTarget, TargetData secondTarget, ProjectManager manager, StringBuilder builder)`

## Parameters


*firstTarget*      First instance of TargetData to compare.

*secondTarget*      Second instance of TargetData to compare.

*manager*      Instance of *ProjectManager*.

*builder*      String builder that will contain information on any checks that fail.

## Return Value


True if these two targets are similar enough to be in the same target family; otherwise, false.

## Remarks


There are a number of checks done:

1.  The Machine of the targets are in the same machine pool.

2.  The Machine of the targets have the same OS Platform.

3.  Both targets are the same target type.

4.  Both targets have common manufacturer/VID/Ven.

5.  Both targets have common driver hash (of all drivers associated with this device, including any upper and lower filters).

6.  Both targets have a common INF hash.

7.  Both targets have the same bus/enumerator type.

8.  Both targets have the same class/subclass.

9.  If DX capable, same DX major version.

10. All targets are on unique machines.

11. If any of the checks fail, the method returns false.

**Note**  
This specifically allows different Device ID, PID (Product Id) or “Dev” and different sub vendor or implementer Ids.

this function populates the event log with additional data if the comparison has failed.

 

## Thread Safety


Any public static (**Shared** in Visual Basic) members of this type are thread safe. Any instance members are not guaranteed to be thread safe.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20TargetFamliy.TargetsAreValidInSameTargetFamily%28StringBuilder%29%20Method%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



