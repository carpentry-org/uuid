# UUID

A simple UUID library and data type for Carp, conforming to RFC 4122,
generatable in version 1 and 4 for now.

## Usage

You’ll be able to pull in the library using:

```clojure
(load "git@github.com:carpentry-org/uuid@0.0.3")
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

<hr/>

Have fun!
