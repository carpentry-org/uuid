# UUID

A simple UUID library and data type for Carp, conforming to RFC 4122,
generatable only in version 4 for now.

## Usage

You’ll be able to pull in the library using:

```clojure
(load "git@github.com:carpentry-org/uuid@0.0.2")
```

You’ll then have access to the functions:
* `UUID.str`, which transforms it into a human-readable format, as defined in
  RFC 4122,
* `UUID.valid?`, which checks whether a string is a valid UUID,
* `UUID.parse`, which parses a string into a UUID data type (returning a
  `Maybe`), and
* `UUID4.generate`, which generates a random UUID, conforming to UUID version 4.

## Caveats

UUIDs in version 1 cannot be generated at the moment, and this library depends
on a as of yet [unmerged feature](https://github.com/carp-lang/Carp/pull/600)
in Carp.

<hr/>

Have fun!
