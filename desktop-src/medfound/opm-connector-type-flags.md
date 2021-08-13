---
description: The values in the following table specify the type of physical connector for a video output.
ms.assetid: 93e816fb-1b40-4865-9c0c-24d96c83fb7f
title: OPM Connector Type Flags (Opmapi.h)
ms.topic: reference
ms.date: 05/31/2018
---

# OPM Connector Type Flags

The values in the following table specify the type of physical connector for a video output.



| Constant/value                                                                                                                                                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span id="OPM_CONNECTOR_TYPE_OTHER"></span><span id="opm_connector_type_other"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_OTHER**</dt> <dt>-1</dt> </dl>                                                                    | Indicates a type of physical connector that is not on this list.<br/>                                                                                                                                                                                                                                                                                                                                                                                                  |
| <span id="OPM_CONNECTOR_TYPE_VGA"></span><span id="opm_connector_type_vga"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_VGA**</dt> <dt>0</dt> </dl>                                                                           | Video Graphics Array (VGA) connector.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                             |
| <span id="OPM_CONNECTOR_TYPE_SVIDEO"></span><span id="opm_connector_type_svideo"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_SVIDEO**</dt> <dt>1</dt> </dl>                                                                  | S-Video connector.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| <span id="OPM_CONNECTOR_TYPE_COMPOSITE_VIDEO"></span><span id="opm_connector_type_composite_video"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_COMPOSITE\_VIDEO**</dt> <dt>2</dt> </dl>                                      | Composite video connector.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <span id="OPM_CONNECTOR_TYPE_COMPONENT_VIDEO"></span><span id="opm_connector_type_component_video"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_COMPONENT\_VIDEO**</dt> <dt>3</dt> </dl>                                      | Component video connector.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <span id="OPM_CONNECTOR_TYPE_DVI"></span><span id="opm_connector_type_dvi"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_DVI**</dt> <dt>4</dt> </dl>                                                                           | Digital video interface (DVI) connector.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                          |
| <span id="OPM_CONNECTOR_TYPE_HDMI"></span><span id="opm_connector_type_hdmi"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_HDMI**</dt> <dt>5</dt> </dl>                                                                        | High-definition multimedia interface (HDMI) connector.<br/>                                                                                                                                                                                                                                                                                                                                                                                                            |
| <span id="OPM_CONNECTOR_TYPE_LVDS"></span><span id="opm_connector_type_lvds"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_LVDS**</dt> <dt>6</dt> </dl>                                                                        | Low voltage differential signaling (LVDS) connector or MIPI Digital Serial Interface (DSI).<br/> A connector using the LVDS or MIPI Digital Serial Interface (DSI) interface to connect internally to a display device. The connection between the graphics adapter and the display device is permanent, non-removable, and not accessible to the user. Applications should not enable High-Bandwidth Digital Content Protection (HDCP) for this connector.<br/> |
| <span id="OPM_CONNECTOR_TYPE_D_JPN"></span><span id="opm_connector_type_d_jpn"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_D\_JPN**</dt> <dt>8</dt> </dl>                                                                    | Japanese D connector. (A connector conforming to the EIAJ RC-5237 standard.)<br/>                                                                                                                                                                                                                                                                                                                                                                                      |
| <span id="OPM_CONNECTOR_TYPE_SDI"></span><span id="opm_connector_type_sdi"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_SDI**</dt> <dt>9</dt> </dl>                                                                           | SDI (serial digital image) connector.<br/>                                                                                                                                                                                                                                                                                                                                                                                                                             |
| <span id="OPM_CONNECTOR_TYPE_DISPLAYPORT_EXTERNAL"></span><span id="opm_connector_type_displayport_external"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_DISPLAYPORT\_EXTERNAL**</dt> <dt>10</dt> </dl>                      | A display port that connects externally to a display device.<br/>                                                                                                                                                                                                                                                                                                                                                                                                      |
| <span id="OPM_CONNECTOR_TYPE_DISPLAYPORT_EMBEDDED"></span><span id="opm_connector_type_displayport_embedded"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_DISPLAYPORT\_EMBEDDED**</dt> <dt>11</dt> </dl>                      | An embedded display port that connects internally to a display device. Also known as an *integrated* display port.<br/> Applications should not enable High-Bandwidth Digital Content Protection (HDCP) for embedded display ports.<br/>                                                                                                                                                                                                                         |
| <span id="OPM_CONNECTOR_TYPE_UDI_EXTERNAL"></span><span id="opm_connector_type_udi_external"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_UDI\_EXTERNAL**</dt> <dt>12</dt> </dl>                                              | A Unified Display Interface (UDI) that connects externally to a display device.<br/>                                                                                                                                                                                                                                                                                                                                                                                   |
| <span id="OPM_CONNECTOR_TYPE_UDI_EMBEDDED"></span><span id="opm_connector_type_udi_embedded"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_UDI\_EMBEDDED**</dt> <dt>13</dt> </dl>                                              | An embedded UDI that connects internally to a display device. Also known as an *integrated* UDI.<br/>                                                                                                                                                                                                                                                                                                                                                                  |
| <span id="OPM_CONNECTOR_TYPE_RESERVED"></span><span id="opm_connector_type_reserved"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_RESERVED**</dt> <dt>14</dt> </dl>                                                           | Reserved for future use.<br/> Supported in Windows 8.1 and later.<br/>                                                                                                                                                                                                                                                                                                                                                                                           |
| <span id="OPM_CONNECTOR_TYPE_MIRACAST"></span><span id="opm_connector_type_miracast"></span><dl> <dt>**OPM\_CONNECTOR\_TYPE\_MIRACAST**</dt> <dt>15</dt> </dl>                                                           | A Miracast wireless connector.<br/> Supported in Windows 8.1 and later.<br/>                                                                                                                                                                                                                                                                                                                                                                                     |
| <span id="OPM_COPP_COMPATIBLE_CONNECTOR_TYPE_INTERNAL"></span><span id="opm_copp_compatible_connector_type_internal"></span><dl> <dt>**OPM\_COPP\_COMPATIBLE\_CONNECTOR\_TYPE\_INTERNAL**</dt> <dt>0x80000000</dt> </dl> | Internal connector. The connection between the graphics adapter and the display device is permanent and not accessible to the user. This flag is used only in *COPP emulation mode*. It can be combined with the other values.<br/>                                                                                                                                                                                                                                    |



## Remarks

If a connector is described as *embedded* or *integrated*, it implies that the connector is internal. These connectors have "EMBEDDED" in the name of the enumeration constant.

Applications should ignore the **OPM\_COPP\_COMPATIBLE\_CONNECTOR\_TYPE\_INTERNAL** flag and instead check for connector types with "EMBEDDED" in the constant name.

With the exception of **OPM\_COPP\_COMPATIBLE\_CONNECTOR\_TYPE\_INTERNAL**, the values listed here are not bit flags, and cannot be combined.

Some of these values are equivalent to values from the **COPP\_ConnectorType** enumeration used in Certified Output Protection Protocol (COPP).

## Requirements



| Requirement | Value |
|-------------------------------------|-------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows Vista \[desktop apps only\]<br/>                                      |
| Minimum supported server<br/> | Windows Server 2008 \[desktop apps only\]<br/>                                |
| Header<br/>                   | <dl> <dt>Opmapi.h</dt> </dl> |



## See also

<dl> <dt>

[OPM Enumerations](opm-enumerations.md)
</dt> </dl>

 

 



