# UUID

A simple UUID library and data type for Carp, conforming to RFC 4122 (and
RFC 9562 for version 7), generatable in version 1, 3, 4, 5, and 7 for now.

## Usage

You’ll be able to pull in the library using:

```clojure
(load "git@github.com:carpentry-org/uuid@0.0.7")
```

You’ll then have access to the functions:
* `UUID.str`, which transforms it into a human-readable format, as defined in
  RFC 4122,
* `UUID.valid?`, which checks whether a string is a valid UUID,
* `UUID.parse`, which parses a string into a UUID data type (returning a
  `Maybe`),
* `UUID.nil` and `UUID.max`, the special all-zero Nil UUID and all-one Max UUID
  defined in RFC 9562 (§5.9 and §5.10), along with the `UUID.nil?` and
  `UUID.max?` predicates that test for them, and
* `UUID4.generate`, which generates a random UUID, conforming to UUID version 4.
* `UUID1.generate`, which generates a time-based UUID conforming to UUID
  version 1: a 60-bit count of 100-nanosecond intervals since
  1582-10-15 00:00:00 UTC, a clock sequence, and a node. The node is always
  random rather than a hardware address, which section 4.5 of RFC 4122 allows.
* `UUID1.timestamp`, which extracts that 60-bit timestamp back out of a
  version-1 UUID (as a `Uint64`), and `UUID1.to-nanotime`, which converts such a
  timestamp to nanoseconds since the Unix epoch — the scale `System.nanotime`
  uses, and the one you can compare against a wall clock.
* `UUID3.generate`, which generates a name-based UUID conforming to UUID
  version 3 (RFC 9562 §5.3): the MD5 hash of a namespace UUID followed by a
  name, truncated to 128 bits. Version 3 is specified over MD5, which is no
  longer considered secure; it is here to interoperate with names already
  registered under an existing version-3 namespace, and `UUID5.generate` or
  `UUID7.generate` are the better choice for new work:

  ```clojure
  (UUID.str &(UUID3.generate &(UUID.namespace-dns) "www.example.com"))
  ; => "5df41881-3aed-3515-88a7-2f4a814cf09e"
  ```
* `UUID5.generate`, which generates a name-based UUID conforming to UUID
  version 5 (RFC 9562 §5.5): the SHA-1 hash of a namespace UUID followed by a
  name, truncated to 128 bits. The same namespace and name always yield the
  same UUID, which makes version 5 the one to reach for when you need
  deterministic, content-derived identifiers:

  ```clojure
  (UUID.str &(UUID5.generate &(UUID.namespace-dns) "www.example.com"))
  ; => "2ed6657d-e927-568b-95e1-2665a8aea6a2"
  ```
* `UUID.namespace-dns`, `UUID.namespace-url`, `UUID.namespace-oid`, and
  `UUID.namespace-x500`, the four predefined namespaces from RFC 9562 §6.6 that
  `UUID3.generate` and `UUID5.generate` take as their first argument — though
  any UUID will do.
* `UUID7.generate`, which generates a time-ordered UUID conforming to UUID
  version 7 (RFC 9562): a 48-bit Unix millisecond timestamp followed by a
  monotonic counter and random bits. Successive UUIDs sort in creation order
  under `UUID.<`, even when generated within the same millisecond, which makes
  them well suited as database keys.
* `UUID7.timestamp`, which extracts the millisecond timestamp back out of a
  version-7 UUID (as a `Uint64`).
* `UUID.<`, `UUID.>`, `UUID.<=`, and `UUID.>=`, which compare two UUIDs as
  unsigned big-endian 128-bit integers (byte by byte), ordering version-7 UUIDs
  chronologically.
* `UUID.hash`, which lets you use UUIDs as keys in a `Map` or `Set`.

<hr/>

Have fun!
