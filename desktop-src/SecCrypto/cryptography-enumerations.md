---
description: The following enumerations are used by cryptography functions and methods.
ms.assetid: 305038c0-754d-4406-9689-716d11964700
title: Cryptography Enumerations
ms.topic: article
ms.date: 05/31/2018
---

# Cryptography Enumerations

The following enumerations are used by cryptography functions and methods.



| Enumeration                                                                                      | Description                                                                                                                                                                                                                                                                                     |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**CAPICOM\_ACTIVE\_DIRECTORY\_SEARCH\_LOCATION**](capicom-active-directory-search-location.md) | Indicates the location to be searched for an Active Directory [*certificate store*](../secgloss/c-gly.md).                                                                                                                            |
| [**CAPICOM\_ATTRIBUTE**](capicom-attribute.md)                                                  | Defines the kind of attribute associated with a [*signature*](../secgloss/d-gly.md).                                                                                                                                                  |
| [**CAPICOM\_CERT\_INFO\_TYPE**](capicom-cert-info-type.md)                                      | Defines what information is to be queried from a certificate.                                                                                                                                                                                                                                   |
| [**CAPICOM\_CERTIFICATE\_FIND\_TYPE**](capicom-certificate-find-type.md)                        | Defines the type of search criteria used to find specific certificates.                                                                                                                                                                                                                         |
| [**CAPICOM\_CERTIFICATE\_INCLUDE\_OPTION**](capicom-certificate-include-option.md)              | Defines which certificates in a chain are saved.                                                                                                                                                                                                                                                |
| [**CAPICOM\_CERTIFICATE\_SAVE\_AS\_TYPE**](capicom-certificate-save-as-type.md)                 | Defines the format of a file that contains certificate information.                                                                                                                                                                                                                             |
| [**CAPICOM\_CERTIFICATES\_SAVE\_AS\_TYPE**](capicom-certificates-save-as-type.md)               | Defines the format of a file that contains certificates information.                                                                                                                                                                                                                            |
| [**CAPICOM\_CHECK\_FLAG**](capicom-check-flag.md)                                               | Defines the conditions for which a certificate chain is to be checked.                                                                                                                                                                                                                          |
| [**CAPICOM\_EKU**](capicom-eku.md)                                                              | Defines the extended key usage names based on where they can be used.                                                                                                                                                                                                                           |
| [**CAPICOM\_ENCODING\_TYPE**](capicom-encoding-type.md)                                         | Indicates the encoding type used.                                                                                                                                                                                                                                                               |
| [**CAPICOM\_ENCRYPTION\_ALGORITHM**](capicom-encryption-algorithm.md)                           | Defines the algorithms to be used in encryption and decryption.                                                                                                                                                                                                                                 |
| [**CAPICOM\_ENCRYPTION\_KEY\_LENGTH**](capicom-encryption-key-length.md)                        | Defines the [*key length*](../secgloss/k-gly.md) to be used in encryption.                                                                                                                                                                          |
| [**CAPICOM\_ERROR\_CODE**](capicom-error-code.md)                                               | Defines error codes that are returned by CAPICOM.                                                                                                                                                                                                                                               |
| [**CAPICOM\_EXPORT\_FLAG**](capicom-export-flag.md)                                             | Defines if any private key export errors are ignored.                                                                                                                                                                                                                                           |
| [**CAPICOM\_HASH\_ALGORITHM**](capicom-hash-algorithm.md)                                       | Defines a hash algorithm.                                                                                                                                                                                                                                                                       |
| [**CAPICOM\_KEY\_ALGORITHM**](capicom-key-algorithm.md)                                         | Defines key algorithms.                                                                                                                                                                                                                                                                         |
| [**CAPICOM\_KEY\_LOCATION**](capicom-key-location.md)                                           | Defines key location types.                                                                                                                                                                                                                                                                     |
| [**CAPICOM\_KEY\_SPEC**](capicom-key-spec.md)                                                   | Defines key specifications.                                                                                                                                                                                                                                                                     |
| [**CAPICOM\_KEY\_STORAGE\_FLAG**](capicom-key-storage-flag.md)                                  | Defines key storage flags.                                                                                                                                                                                                                                                                      |
| [**CAPICOM\_KEY\_USAGE**](capicom-key-usage.md)                                                 | Defines the ways in which a key can be used.                                                                                                                                                                                                                                                    |
| [**CAPICOM\_OID**](capicom-oid.md)                                                              | Provides the names for CAPICOM object identifiers.                                                                                                                                                                                                                                              |
| [**CAPICOM\_PROPID**](capicom-propid.md)                                                        | Defines the CAPICOM property identifiers.                                                                                                                                                                                                                                                       |
| [**CAPICOM\_PROV\_TYPE**](capicom-prov-type.md)                                                 | Specifies the type of [*cryptographic service provider*](../secgloss/c-gly.md).                                                                                                                             |
| [**CAPICOM\_SECRET\_TYPE**](capicom-secret-type.md)                                             | Indicates the kind of secret used to derive a key to be used for encryption or decryption of data.                                                                                                                                                                                              |
| [**CAPICOM\_SIGNED\_DATA\_VERIFY\_FLAG**](capicom-signed-data-verify-flag.md)                   | Indicates the encoding type used.                                                                                                                                                                                                                                                               |
| [**CAPICOM\_STORE\_LOCATION**](capicom-store-location.md)                                       | Indicates the location of a [*certificate store*](../secgloss/c-gly.md).                                                                                                                                                              |
| [**CAPICOM\_STORE\_OPEN\_MODE**](capicom-store-open-mode.md)                                    | Indicates how a certificate store is to be opened.                                                                                                                                                                                                                                              |
| [**CAPICOM\_STORE\_SAVE\_AS\_TYPE**](capicom-store-save-as-type.md)                             | Indicates the encoding of a certificate store.                                                                                                                                                                                                                                                  |
| [**CARD\_DIRECTORY\_ACCESS\_CONDITION**](card-directory-access-condition.md)                    | Specifies access control permissions for a directory on a [*smart card*](../secgloss/s-gly.md).                                                                                                                                                     |
| [**CARD\_FILE\_ACCESS\_CONDITION**](card-file-access-condition.md)                              | Specifies access control permissions for a file on a smart card.                                                                                                                                                                                                                                |
| [**CASetupProperty**](/windows/win32/api/casetup/ne-casetup-casetupproperty)                                         | Specifies a property type for setup and configuration of a [*certification authority*](../secgloss/c-gly.md) (CA) role when using the [**ICertSrvSetup**](/windows/desktop/api/Casetup/nn-casetup-icertsrvsetup) interface.                                   |
| [**CEPSetupProperty**](/windows/win32/api/casetup/ne-casetup-cepsetupproperty)                                                     | Specifies a property type that can be set on or retrieved from an [**ICertificateEnrollmentPolicyServerSetup**](/windows/desktop/api/Casetup/nn-casetup-icertificateenrollmentpolicyserversetup) interface.                                                                                                                         |
| [**CESSetupProperty**](/windows/win32/api/casetup/ne-casetup-cessetupproperty)                                                     | Specifies a property type that can be set on or retrieved from an [**ICertificateEnrollmentServerSetup**](/windows/desktop/api/Casetup/nn-casetup-icertificateenrollmentserversetup) interface.                                                                                                                                     |
| [**CRYPT\_XML\_PROPERTY\_ID**](/windows/desktop/api/Cryptxml/ne-cryptxml-crypt_xml_property_id)                                        | Specifies the type and usage of the XML property.                                                                                                                                                                                                                                               |
| [**CRYPT\_XML\_CHARSET**](/windows/desktop/api/Cryptxml/ne-cryptxml-crypt_xml_charset)                                                 | Used to specify the character set used in the XML.                                                                                                                                                                                                                                              |
| [**CRYPT\_XML\_KEYINFO\_SPEC**](/windows/desktop/api/Cryptxml/ne-cryptxml-crypt_xml_keyinfo_spec)                                      | Specifies values for the *dwKeyInfoSpec* parameter in the [**CryptXmlSign**](/windows/desktop/api/Cryptxml/nf-cryptxml-cryptxmlsign) function.                                                                                                                                                                                        |
| [**ENUM\_CATYPES**](/windows/desktop/api/Certsrv/ne-certsrv-enum_catypes)                                                            | Specifies a [*certification authority*](../secgloss/c-gly.md) (CA) type.                                                                                                                                                  |
| [**ENUM\_PERIOD**](/windows/desktop/api/celib/ne-celib-enum_period)                                                              | Specifies the units of a time span.                                                                                                                                                                                                                                                             |
| [**KEYSVC\_TYPE**](keysvc-type.md)                                                              | Indicates whether a key applies to a computer or a service.                                                                                                                                                                                                                                     |
| [**MSCEPSetupProperty**](/windows/win32/api/casetup/ne-casetup-mscepsetupproperty)                                                 | Specifies a property type for setup and configuration of a Microsoft [*Simple Certificate Enrollment Protocol*](../secgloss/s-gly.md) (SCEP) role using [**IMSCEPSetup**](/windows/desktop/api/Casetup/nn-casetup-imscepsetup). |



 

 

 