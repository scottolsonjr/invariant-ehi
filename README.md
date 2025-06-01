# The Invariant EHI Project

The invariant storage system provides secure, distributed storage for any content an application may wish to persist.
This project explore use of the invariant storage system to persist personal, electronic health information (EHI).

## Goals

The goals of this exploration and conceptual design include:

1. A Patient must be able to securely store their health information from payers, providers, and others.
2. The service providing the storage must not be able to read the EHI mitigating risk of breach due to compromise of the storage system.
3. The service providing the business logic does not require persistence of EHI outside of the storage system removing another vector for unauthorized access.
4. EHI stored in the storage system is encrypted by the Patient and may only be decrypted by the Patient. (preferrably on device)
5. EHI stored in the storage system is searchable by the Patient.
6. The Patient can allow multiple applications to access their stored EHI including granting and revoking access.
7. The Patient can export all stored EHI and remove as desired.

## The Invariant Project

The [Invariant Project](https://github.com/chuckjaz/invariant) specification is currently under development.
The specification currently includes multiple "servers" filling different roles within the storage system.

- The [Storage Servers](https://github.com/chuckjaz/invariant/blob/main/src/storage/Storage.md) handle the storage of the invariant data.
- The [Slot Servers](https://github.com/chuckjaz/invariant/blob/main/src/slots/Slots.md) support identification of the current and previous versions of invariant data.
- The [Broker Servers](https://github.com/chuckjaz/invariant/blob/main/src/broker/Broker.md) support the discovery of endpoint and authorization of requests made to various servers.
- The [Find Servers](https://github.com/chuckjaz/invariant/blob/main/src/find/Find.md) supports the discovery of storage service that may contain a blob or a broker server that contains information about a specific server.
- The [Files Servers](https://github.com/chuckjaz/invariant/blob/main/src/files/files.md) support the implementation of a POSIX-style file system for interaction with the stored invariant data.
- The [Production Servers](https://github.com/chuckjaz/invariant/blob/main/src/productions/productions.md) supports the transformation and storage of invariant data.
- The [Names Servers](https://github.com/chuckjaz/invariant/blob/main/src/names/Name.md) support use of DNS to map names to addresses.

Supporting services include:

- The [Distributor Services](https://github.com/chuckjaz/invariant/blob/main/src/distribute/distribute.md) manage the distribution of invariant data across storage servers to ensure high availability.

## Electronic Health Information (EHI)

We will use the [HL7 FHIR R4](https://www.hl7.org/fhir/R4/) specification to define the stored electronic health information.
Although intended for exchange rather than storage it will provide a common reference for these concepts.
Other health information standards as well as proprietary formats could be used, however use of a shared standard will help with portability.

### Profile Support

The invariant storage system will not place constraints on the profiles the stored FHIR resources may conform to.
The project will use profiles from the following Implementation Guides to determine the scope of data to account for:

- The [US Core Implementation Guide](https://www.hl7.org/fhir/us/core/) defines what information must be available to the Patient from Healthcare Providers.
- The [Da Vinci Payer Data Exchange](https://www.hl7.org/fhir/us/davinci-pdex/index.html) and [CARIN Consumer Directed Payer Exchange](https://www.hl7.org/fhir/us/carin-bb/) define what information must be available to the Patient from healthcare Payers. 

The use of US-based Implementation Guides in this specification is not intended to exclude use of other international and national implementation guides with the invariant storage system.
