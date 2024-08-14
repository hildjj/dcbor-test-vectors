# dCBOR Test Vectors

These vectors are intended to test
[draft-mcnally-deterministic-cbor](https://www.ietf.org/archive/id/draft-mcnally-deterministic-cbor-11.txt).

## Valid

Valid tests are in the following form:

```ts
interface Valid {
  cbor: string,        // Base64-encoded
  hex: string,         // Hex-encoded, same binary data as the cbor field
  decoded?: unknown,   // For tests that can be expressed as JSON.
  diagnostic: string,  // CBOR diagnostic notation
  roundtrip?: boolean, // If true, encode(decode(hex)) = hex
  notes?: string,      // Why this test is interesting, if provided
}

export type ValidDcborTests = Valid[];
```

To fully check each of these vectors, perform the following operations:

- Ensure that `Base64Decode(cbor) = HexDecode(cbor)` (optional)
- dCBOR decode either `cbor` or `hex`.
  - If `decoded` is provided, ensure the result matches `decoded`.
  - If `roundtrip` is true, ensure that dCBOR encoding the result matches
    the original binary data
- Decode either `cbor` or `hex` to diagnostic format in dCBOR mode.
  - Ensure the result matches `diagnostic`
- No errors should fire for any of these inputs.

## Invalid

Invalid tests are in the form:

```ts
interface Invalid {
  value: string,       // For reference only
  hex: string,         // Hex-encoded binary dCBOR input
  notes?: string,      // Why this test is interesting, if provided
}

export type InvalidDcborTests = Invalid[];
```

To check each of these vectors:

- dCBOR decode `hex`.
  - Ensure that an error was reported

## Provenance

The original source for the first checkin of these vectors was
[draft-mcnally-deterministic-cbor-11](https://www.ietf.org/archive/id/draft-mcnally-deterministic-cbor-11.txt).
