# Electronic Health Information (EHI)

This specification uses the [HL7 FHIR R4](https://www.hl7.org/fhir/R4/) specification to define the structure of the stored EHI.

## Types of EHI

The following files will be considered EHI as part of the solution:

- [Resources](./resources/README.md): The NDJSON files storing the health information.
- [Indexes](./indexes/README.md): The index files containing portions of the EHI for use with searching.
- [Manifest](./manifest/README.md): Optional. If saved to a Storage server it will be treated as EHI as it provides discoverability of the EHI.

Each of the above will be associated with a Slot and the Slot will reference the current and previous versions of the file.

## Encryption Methods

We will use JSON Web Encryption (JWE) to encrypt the EHI.

- The file/blob will be encrypted using AES (e.g., A256GSM).
- The AES (symmetric) key will be encrypted using ECC (preferred) or RSA. (e.g., ECDH-ES, RSA-OAEP).
- The `AES_128_CBC_HMAC_SHA_256` algorithm will be used to create the Authentication Tag.

### Protected Header

The following parameters are to be used when constructing the JWE.

- `alg` (required): The cryptographic algorithm used to encrypt the AES symmetric key.
- `enc` (required): The encryption algorithm used to encrypt the content and produce the ciphertext.
- `zip` (recommended): The compression algorithm used on the content before encryption.
- `kid` (recommended): The id of the key used to encrypt the content. Can be used to determine the private key needed to decrypt. Alternatives include: `jku`, `jwk`, `x5u`, `x5c`, and `x5t`.
- `typ` (optional): Essentially, JWE.
- `cty` (recommended): MIME type of the content. E.g., `application/fhir+ndjson`, `application/json`, etc.

The `crit` header is not currently supported but may be added in the future if custom headers are to be defined.
For example, if we want to exppose the resource type of the NDJSON blob or the search parameter and index type of an index blob.

### Stored Format

Unless performance improvements are identified in the future, this specification will prefer the JWE JSON Serialization `application/jose+json` format without line breaks and extra spaces for storing the JWE.

```json
{
    "protected": "eyJ...",
    "encrypted_key": "eyJ...",
    "iv": "random",
    "ciphertext": "encryptedblob",
    "tag": 
}
```

The Storage server is expected to set the ID/Address of the stored JWE to the SHA-256 hash of the blob.

The invariant storage system allows for the storing of the signature of the blob and the associated public key.
Our intent is to create a persistent Slot ID that can be continually referenced as the stored blob is updated.
If the signature of the blob is to be tracked, then this will require secure storage of the Ed25519 private key so that the same private key can be used to sign the updated blobs as well.
A separate private key will need to be stored for each slot as the public key serves as the Slot ID.
