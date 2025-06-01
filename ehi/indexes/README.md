# EHI Indexes

We will use indexes to support efficient searching of the stored health information.
These indexes will be stored in a Slot and Storage servers like the resources.

## Storage

Indexes will be stored using JSON Web Encryption (RFC 7516) in a format that most effectively supports the type of index being stored.

## Index Types

Index types will vary based on the type of data to be indexed.

- Hash Index: Used for id, identifier, and coded values.
- B-Tree Index: Used for ranged indexes like dates.

### FHIR Search Parameter Mapping

HL7 defines a number of different search parameter types which we will use to help define our indexing strategy.

| Search Parameter Type | Index Type | Considerations |
| --------------------- | ---------- | -------------- |
| [Number](https://www.hl7.org/fhir/R4/search.html#number)          | B-Tree   | T.B.D. |
| [Date/DateTime](https://www.hl7.org/fhir/R4/search.html#date)     | B-Tree   | There are prefixes that can impact the searching behavior |
| [String](https://www.hl7.org/fhir/R4/search.html#string)          | Inverted | T.B.D. |
| [String](https://www.hl7.org/fhir/R4/search.html#string):contains | Inverted | T.B.D. |
| [String](https://www.hl7.org/fhir/R4/search.html#string):exact    | Inverted | T.B.D. |
| [Token](https://www.hl7.org/fhir/R4/search.html#token)            | Hash     | Need to account for searches with and without system.     |
| [Reference](https://www.hl7.org/fhir/R4/search.html#reference)    | Hash     | Need to account for searches with and without type.       |
| [Composite](https://www.hl7.org/fhir/R4/search.html#composite)    | T.B.D.   | T.B.D. |
| [Quantity](https://www.hl7.org/fhir/R4/search.html#quantity)      | T.B.D.   | T.B.D. |
| [URI](https://www.hl7.org/fhir/R4/search.html#uri)                | Hash     | T.B.D. |
| [Special](https://www.hl7.org/fhir/R4/search.html#special)        | Varies   | Varies |
