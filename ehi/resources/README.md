# FHIR Resources

The documentation and examples for storage of electronic health information (EHI) on the invariant storage system with use resources defined in [HL7 FHIR R4](https://www.hl7.org/fhir/R4/).
The following implementation guides will allowed be referenced to inform available content, potential use cases, and other considerations.

- The [US Core Implementation Guide](https://www.hl7.org/fhir/us/core/) defines what information must be available to the Patient from Healthcare Providers.
- The [Da Vinci Payer Data Exchange](https://www.hl7.org/fhir/us/davinci-pdex/index.html) and [CARIN Consumer Directed Payer Exchange](https://www.hl7.org/fhir/us/carin-bb/) define what information must be available to the Patient from healthcare Payers.

## Storage

Each FHIR resource type will be stored separately as NDJSON files with multiple resources stored per file/blob with limited exceptions:

- Patient is currently intended to store a single Patient to prevent the commingling of records.
- Binary will be one blob per binary to address size and performance constraints.
- Bundle may be one blob per bundle as well to address potential size and performance contraints.

The NDJSON files will be encrypted and stored on the Storage Server using JSON Web Encryption (RFC 7516).

## Included Resources

In addition to the [Patient](./Patient.md) resource, the following resources are to be accounted for in this specification:

- AllergyIntolerance
- Binary
- Bundle
- CarePlan
- CareTeam
- Condition
- Coverage
- Device
- DiagnosticReport
- DocumentReference
- Encounter
- ExplanationOfBenefit
- Goal
- Immunization
- Location
- Medication
- MedicationDispense
- MedicationRequest
- Observation
- Organization
- Practitioner
- PractitionerRole
- Procedure
- Provenance
- QuestionnaireResponse
- RelatedPerson
- ServiceRequest
- Specimen

Additional resources for consideration include:

- Appointment
- AppointmentResponse
- EpisodeOfCare
- Media
- MedicationAdministration
- MedicationStatement
- Task
