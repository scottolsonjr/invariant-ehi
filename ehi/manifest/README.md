# Manifest

A manifest file can be used in order to quickly locate the stored resources and indexes.
This file may be stored on the storage servers as well or manages by the application.
We will use the Slot ID to maintain a consistent ID for the current version of the content as the Storage address will change as the resource NDJSON and index files are updated.

Here is a concept of what this manifest could look like.

```json
{
    "resource": {
        "patient": {
            "slot": [
                ":slot-id"
            ],
            "searchParam": {
                "_id": ":slot-id",
                "birthdate": ":slot-id"
            }
        }
    }
}
```

If we pursue closer alignment with the [FHIR CapabilityStatement](https://www.hl7.org/fhir/R4/capabilitystatement.html) then the manifest could look more like this.

```json
{
    "resource": [
        {
            "type": "Patient",
            "slot": [
                ":slot-id"
            ],
            "searchParam": [
                {
                    "name": "_id",
                    "type": "token",
                    "slot": ":slot-id"
                },
                {
                    "name": "birthdate",
                    "type": "date",
                    "slot": ":slot-id"
                }
            ]
        }
    ]
}
```
