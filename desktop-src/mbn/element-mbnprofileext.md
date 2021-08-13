---
Description: MBNProfileExt
MS-HAID: WWAN\_profile\_v4.element\_MBNProfileExt
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/desktop
title: MBNProfileExt
ms.topic: reference
ms.date: 05/31/2018
---

# <span id="WWAN_profile_v4.element_MBNProfileExt"></span>MBNProfileExt

The **MBNProfileExt** element is an extension of the earlier MBNProfile element. It identifies a Mobile Broadband profile with a richer set of options than the MBNProfile element.

There can be more than one MbnProfileExt element in a profile, describing profile settings for a particular set of operating conditions. Use the [**ProfileConditionedOn**](element-profileconditionedon.md) child element of **MBNProfileExt** to specify which operating conditions make a particular profile the active profile.

## Element hierarchy

**<MBNProfileExt>**

## Syntax

``` syntax
<MBNProfileExt>

  <!-- Child elements -->
  Name,
  Description?,
  ICONFilePath?,
  IsDefault,
  ProfileCreationType?,
  SubscriberID?,
  SimIccID,
  HomeProviderName?,
  AutoConnectOnInternet?,
  ConnectionMode?,
  Context?,
  DataRoamingPartners?,
  PurposeGroups?,
  ProfileConditionedOn?,
  IsProvisioningProfile?,
  ApnID?,
  AdminEnable?,
  AdminRoamControl?,
  IsExclusiveToOther?,
  IsLongStandingAdditionalPdpContextProfile?,
  MmsConfiguration?,
  any element in a non-schema namespace*

</MBNProfileExt>
```

### Key

`?`   optional (zero or one)

`*`   optional (zero or more)

## <span id="Attributes_and_Elements"></span><span id="attributes_and_elements"></span><span id="ATTRIBUTES_AND_ELEMENTS"></span>Attributes and Elements

### <span id="attributes"></span><span id="ATTRIBUTES"></span>Attributes

None.

### <span id="Child_Elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>Child Elements

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Child Element</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="element-adminenable.md">AdminEnable</a></td>
<td><p>Specifies whether the profile is enabled administratively.This is a new element for v4.</p></td>
</tr>
<tr class="even">
<td><a href="element-adminroamcontrol.md">AdminRoamControl</a></td>
<td><p>Specifies whether the profile is administratively roam controlled. This element is new for v4. The value of this element is a <a href="simpletype-roamcontroltype.md"><strong>roamControlType</strong></a> value. This is an optional element; if no value is specified, then <strong>AllRoamAllowed</strong> is the default.</p></td>
</tr>
<tr class="odd">
<td><a href="element-apnid.md">ApnID</a></td>
<td><p>An APN ID associated with this profile.This element is new in v4, and it is optional.</p></td>
</tr>
<tr class="even">
<td><a href="element-autoconnectoninternet.md">AutoConnectOnInternet</a></td>
<td><p>Specifies whether the Mobile Broadband device will automatically connect to a network.</p>
<p>For more information, see the documentation for the v1 <a href="../mbn/schema-autoconnectoninternet-mbnprofile-element.md"><strong>AutoConnectOnInternet</strong></a> element.</p></td>
</tr>
<tr class="odd">
<td><a href="element-connectionmode.md">ConnectionMode</a></td>
<td><p>Specifies the auto connection setting to be used for a Mobile Broadband device.</p>
<p>For more information, see the documentation for the v1 <a href="../mbn/schema-connectionmode-mbnprofile-element.md"><strong>ConnectionMode</strong></a> element.</p></td>
</tr>
<tr class="even">
<td><a href="element-context.md">Context</a></td>
<td><p>Specifies the parameters required to establish a data connection.</p></td>
</tr>
<tr class="odd">
<td><a href="element-dataroamingpartners.md">DataRoamingPartners</a></td>
<td><p>Specifies a list of preferred network providers when roaming.</p>
<p>For details, see the documentation for the v1 <a href="../mbn/schema-dataroamingpartners-mbnprofile-element.md"><strong>DataRoamingPartners</strong></a> element.</p></td>
</tr>
<tr class="even">
<td><a href="element-description.md">Description</a></td>
<td><p>A description of the profile.</p></td>
</tr>
<tr class="odd">
<td><a href="element-homeprovidername.md">HomeProviderName</a></td>
<td><p>The name of the home provider for the given SIM/Device. For more information, see the documentation for the v1 <a href="../mbn/schema-homeprovidername-mbnprofile-element.md"><strong>HomeProviderName</strong></a> element.</p></td>
</tr>
<tr class="even">
<td><a href="element-iconfilepath.md">ICONFilePath</a></td>
<td><p>The path to the icon file for the connection. The operating system connection user interface displays the icon when a connection is made using this profile.</p>
<p>For more details on using this element, see the v1 documentation for <a href="../mbn/schema-iconfilepath-mbnprofile-element.md"><strong>ICONFilePath</strong></a>.</p></td>
</tr>
<tr class="odd">
<td><a href="element-isdefault.md">IsDefault</a></td>
<td><p>Specifies whether this profile is the default profile.</p>
<p>For more detail on this element, see the v1 documentation for <a href="../mbn/schema-isdefault-mbnprofile-element.md"><strong>IsDefault</strong></a>.</p></td>
</tr>
<tr class="even">
<td><a href="element-isexclusivetoother.md">IsExclusiveToOther</a></td>
<td><p>Specifies that this profile is exclusive to other profiles of the same profile set(s).This element is new for v4.</p></td>
</tr>
<tr class="odd">
<td><a href="element-islongstandingadditionalpdpcontextprofile.md">IsLongStandingAdditionalPdpContextProfile</a></td>
<td><p>Specifies that this profile is a long-standing additional PDP context profile.If the value of this element is <strong>true</strong>, then <a href="../WWAN_profile_v3/element_IsAdditionalPdpContextProfile.md"><strong>IsAdditionalPdpContextProfile</strong></a> must also be set to <strong>true</strong>. This is a new element for v4.</p></td>
</tr>
<tr class="even">
<td><a href="element-isprovisioningprofile.md">IsProvisioningProfile</a></td>
<td><p>Specifies that this profile is to be used for provisioning only.Otherwise, the profile is not applicable, and cannot be used to activate a Packet Data Protocol (PDP) context. This element is new for v4.</p>
<p>If <strong>IsProvisioningProfile</strong> is true, <a href="element-isdefault.md"><strong>IsDefault</strong></a> must be false, and <a href="element-connectionmode.md"><strong>ConnectionMode</strong></a> must be manual.</p></td>
</tr>
<tr class="odd">
<td><a href="element-mmsconfiguration.md">MmsConfiguration</a></td>
<td><p>Configuration information for Multimedia Messaging Service (MMS).</p>
<p>In addition to setting the configuration elements within this element, an MMS profile must have the following settings.</p>
<ul>
<li>Its <a href="element-name.md"><strong>Name</strong></a> element must contain a system-wide unique name.</li>
<li>Its <a href="../mbn/schema-profilecreationtype-mbnprofile-element.md"><strong>ProfileCreationType</strong></a> must be set to <strong>UserProvisioned</strong>.</li>
<li>Its <a href="https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnsubscriberinformation-get_simiccid"><strong>SimIccID</strong></a> must contain the ICCID of the SIM that this profile is intended for.</li>
<li>Its <a href="../mbn/schema-connectionmode-mbnprofile-element.md"><strong>ConnectionMode</strong></a> must be set to <strong>Manual</strong>.</li>
<li>Its <a href="element-purposegroupguid.md"><strong>PurposeGroupGuid</strong></a> must contain the GUID for MMS purpose group.</li>
<li>Its <a href="../WWAN_profile_v3/element_IsAdditionalPdpContextProfile.md"><strong>IsAdditionalPdpContextProfile</strong></a> must be set to <strong>true</strong>.</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="element-name.md">Name</a></td>
<td><p>The name of the profile. For more information, see the documentation for the v1 <a href="../mbn/schema-name-mbnprofile-element.md"><strong>Name</strong></a> element.</p></td>
</tr>
<tr class="odd">
<td><a href="element-profileconditionedon.md">ProfileConditionedOn</a></td>
<td><p>Specifies the conditions which must be satisfied for a profile to be applicable.</p>
<p>This element is new for v4. It enables you to specify multiple profiles that apply in different conditions, and for the proper profile to be used automatically when it is applicable. This element is optional. If you do not specify it, then the profile is always applicable with respect to the conditions listed.</p></td>
</tr>
<tr class="even">
<td><a href="element-profilecreationtype.md">ProfileCreationType (in MBNProfileExt)</a></td>
<td><p>Specifies the creator of the profile.</p>
<p>For more information about this element, see the documentation for the v1 <a href="../mbn/schema-profilecreationtype-mbnprofile-element.md"><strong>ProfileCreationType</strong></a> element.</p></td>
</tr>
<tr class="odd">
<td><a href="element-purposegroups.md">PurposeGroups</a></td>
<td><p>An optional list of groups of profiles, where each group includes profiles used for a common purpose.</p>
<p>This element is new for v4 of the schema.</p>
<p>One profile can be listed in multiple groups.</p></td>
</tr>
<tr class="even">
<td><a href="element-simiccid.md">SimIccID</a></td>
<td><p>The SIM Identifcation number for GSM devices. For more details , see the documentation for the v1 <a href="https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnsubscriberinformation-get_simiccid"><strong>SimIccID</strong></a> element.</p></td>
</tr>
<tr class="odd">
<td><a href="element-subscriberid.md">SubscriberID</a></td>
<td><p>Identifies the unique identifier of the profile.</p>
<p>For a GSM network this should contain the IMSI (International Mobile Subscriber Identity) of the SIM and for CDMA devices it should contain the MIN (Mobile Identification Number) of the device.</p>
<p>For more information, see the documentation for the v1 <a href="../mbn/schema-subscriberid-mbnprofile-element.md"><strong>SubscriberID</strong></a> element.</p></td>
</tr>
</tbody>
</table>

 

### <span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>Parent Elements

This outermost (document) element may not be contained by any other elements.

## Requirements

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Namespace</p></td>
<td><p>https://www.microsoft.com/networking/WWAN/profile/v4</p></td>
</tr>
</tbody>
</table>

 

 



