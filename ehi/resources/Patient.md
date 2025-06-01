# Patient

The [Patient resource](https://www.hl7.org/fhir/R4/patient.html) provides demographic and other administrative information about the individual receiving treatment.
This project intentionally constrains the storage to a single patient to provide the intended security and isolation of the EHI.
Essentially, this specification assumes the Patient is the user who secured and encrypted the data.

## Caregivers

This design would allow for caregivers to securely store EHI on behalf of those they care for, including but not limited to:

- Children who are too young to manage their own health care.
- Adults who are unable to manage or have delegated their own health care.
- Animals.

A future goal would be to allow the Patient to own their EHI separate from the caregiver's even when delegated allowing for access to be revoked and/or transferred as needed.
If the caregiver maintains the EHI in their own store then they could potentially:

- Retain the information after their role on the CareTeam is ended
- Prevent the Patient from retaining their record requiring aggregation from payers and providers again.

Designs for sharing access to EHI will come in future work.

## Storage

Unlike other resources, there is intentionally only one Patient resource stored for this patient/user.
This means that the Patient NDJSON should have only one entry in it representing the indivudal who is storing their health information.

## Indexes

Given the single Patient entry in the NDJSON file, indexes are not currently an expected requirement.
However, here are some indexes that may be helpful, in a multi-patient configuration.

| Name | Type | FHIR Search Parameter |
| ---- | ---- | --------------------- |
| `patient_birthdate_idx`  | B-tree   | `birthdate`  |
| `patient_deathdate_idx`  | B-tree   | `death-date` |
| `patient_family_idx`     | Inverted | `family`     |
| `patient_gender_idx`     | Hash     | `gender`     |
| `patient_id_idx`         | Hash     | `_id`        |
| `patient_identifier_idx` | Hash     | `identifier` |
| `patient_name_idx`       | Inverted | `name`       |
