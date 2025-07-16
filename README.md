## null [![GoDoc](https://godoc.org/github.com/goforj/null/v6?status.svg)](https://godoc.org/github.com/guregu/null/v6)

This is a fork of github.com/guregu/null, a library for dealing with nullable SQL and JSON values in Go. It serves as a proxy fork because the original repository has changed names. This pins the package to version 6.

`import "github.com/goforj/null/v6"`

null is a library with reasonable options for dealing with nullable SQL and JSON values

There are two packages: `null` and its subpackage `zero`.

Types in `null` will only be considered null on null input, and will JSON encode to `null`. If you need zero and null be considered separate values, use these.

Types in `zero` are treated like zero values in Go: blank string input will produce a null `zero.String`, and null Strings will JSON encode to `""`. Zero values of these types will be considered null to SQL. If you need zero and null treated the same, use these.

#### Interfaces

- All types implement `sql.Scanner` and `driver.Valuer`, so you can use this library in place of `sql.NullXXX`.
- All types also implement `json.Marshaler` and `json.Unmarshaler`, so you can marshal them to their native JSON representation.
- All non-generic types implement `encoding.TextMarshaler`, `encoding.TextUnmarshaler`. A null object's `MarshalText` will return a blank string.
- All types implement `interface { IsZero() bool }`. Combined with Go 1.24's `,omitzero`, this lets you omit null types from JSON.

## null package

`import "github.com/goforj/null/v6"`

#### null.String
Nullable string.

Marshals to JSON null if SQL source data is null. Zero (blank) input will not produce a null String.

#### null.Int, null.Int32, null.Int16, null.Byte
Nullable int64/int32/int16/byte.

Marshals to JSON null if SQL source data is null. Zero input will not produce a null Int.

#### null.Float
Nullable float64.

Marshals to JSON null if SQL source data is null. Zero input will not produce a null Float.

#### null.Bool
Nullable bool.

Marshals to JSON null if SQL source data is null. False input will not produce a null Bool.

#### null.Time

Marshals to JSON null if SQL source data is null. Zero input will not produce a null Time.

#### null.Value
Generic nullable value.

Will marshal to JSON null if SQL source data is null. Does not implement `encoding.TextMarshaler`.

## zero package

`import "github.com/goforj/null/v6/zero"`

#### zero.String
Nullable string.

Will marshal to a blank string if null. Blank string input produces a null String. Null values and zero values are considered equivalent.

#### zero.Int, zero.Int32, zero.Int16, zero.Byte
Nullable int64/int32/int16/byte.

Will marshal to 0 if null. 0 produces a null Int. Null values and zero values are considered equivalent.

#### zero.Float
Nullable float64.

Will marshal to 0.0 if null. 0.0 produces a null Float. Null values and zero values are considered equivalent.

#### zero.Bool
Nullable bool.

Will marshal to false if null. `false` produces a null Float. Null values and zero values are considered equivalent.

#### zero.Time
Nullable time.

Will marshal to the zero time if null. Uses `time.Time`'s marshaler.

#### zero.Value[`T`]
Generic nullable value.

Will marshal to zero value if null. `T` is required to be a comparable type. Does not implement `encoding.TextMarshaler`.

## About

### Q&A

#### Can you add support for other types?
This package is intentionally limited in scope. It will only support the types that [`driver.Value`](https://godoc.org/database/sql/driver#Value) supports. Feel free to fork this and add more types if you want.

#### Can you add a feature that ____?
This package isn't intended to be a catch-all data-wrangling package. It is essentially finished. If you have an idea for a new feature, feel free to open an issue to talk about it or fork this package, but don't expect this to do everything.

### License
BSD
