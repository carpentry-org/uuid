# UUID

A simple UUID library and data type for Carp, conforming to RFC 4122 (and
RFC 9562 for version 7), generatable in version 1, 4, and 7 for now.

## Usage

You’ll be able to pull in the library using:

```clojure
(load "git@github.com:carpentry-org/uuid@0.0.6")
```

You’ll then have access to the functions:
* `UUID.str`, which transforms it into a human-readable format, as defined in
  RFC 4122,
* `UUID.valid?`, which checks whether a string is a valid UUID,
* `UUID.parse`, which parses a string into a UUID data type (returning a
  `Maybe`), and
* `UUID4.generate`, which generates a random UUID, conforming to UUID version 4.
* `UUID1.generate`, which generates a random UUID, conforming to UUID version 1.
  Currently the interface part of the UUID is always random (conforming to
  section 4.5 of the RFC).
* `UUID7.generate`, which generates a time-ordered UUID conforming to UUID
  version 7 (RFC 9562): a 48-bit Unix millisecond timestamp followed by a
  monotonic counter and random bits. Successive UUIDs sort in creation order
  under `UUID.<`, even when generated within the same millisecond, which makes
  them well suited as database keys.
* `UUID7.timestamp`, which extracts the millisecond timestamp back out of a
  version-7 UUID (as a `Uint64`).
* `UUID.<`, which compares two UUIDs as unsigned big-endian 128-bit integers
  (byte by byte), ordering version-7 UUIDs chronologically.
* `UUID.hash`, which lets you use UUIDs as keys in a `Map` or `Set`.

<hr/>

Have fun!
