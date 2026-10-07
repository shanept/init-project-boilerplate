---
title: Data Notation
document-id: SYSTEM-GOV-DATA-NOTATION
document-type: governance
status: accepted
scope: system
---

# Data Notation

Read this file when defining, changing, reviewing, accepting, or implementing logical data types, field semantics, or boundary representations. Read the [core authoring rules](../SPECIFICATION-AUTHORING-RULES.md) first and follow its routing for any additional concerns.

## Logical data structures

### Portable C-style logical notation

**DATA-NOTATION-RULE-001:** Data structures defined in Markdown specifications must use portable C-style logical notation. This notation defines logical shape and semantics. It does not define implementation details such as memory layout, alignment, calling convention, raw pointers, or serialization encoding.

Example of logical notation, not an application contract:

```c
type RecordId = string;
type ItemIndex = uint32;

struct ReorderItemsRequest {
    required RecordId record_id;
    repeated ItemIndex item_indexes;
    required ItemIndex destination_index;
}
```

**DATA-NOTATION-RULE-002:** Fields are non-nullable by default. Field cardinality is explicit:

- **DATA-NOTATION-RULE-003:** `required` means exactly one non-null value must be present;
- `optional` means the field may be absent but, when present, its value is non-null;
- `nullable` means a present field may contain null; and
- `repeated` means an ordered, variable-length sequence of non-null values.

**DATA-NOTATION-RULE-004:** The combined form `optional nullable` is permitted only when absence and explicit null have different defined meanings. Any use of `nullable` must define the meaning of null. When there is no semantic difference between absence and null, use `optional` and prohibit null.

### Primitive types

**DATA-NOTATION-RULE-005:** The portable primitive types are:

| Type | Meaning |
| --- | --- |
| `bool` | Boolean `true` or `false` |
| `int8`, `int16`, `int32`, `int64` | Signed integer of the stated bit width |
| `uint8`, `uint16`, `uint32`, `uint64` | Unsigned integer of the stated bit width |
| `float32` | IEEE 754 binary32 value |
| `float64` | IEEE 754 binary64 value |
| `decimal(P, S)` | Exact base-10 value with precision `P` and scale `S` |
| `string` | Unicode text; encoding is defined by the applicable boundary |
| `bytes` | Opaque sequence of bytes |

**DATA-NOTATION-RULE-006:** Ambiguous or representation-dependent types such as `char`, `short`, `int`, `long`, `long long`, `unsigned`, `size_t`, `float`, `double`, and `void *` are prohibited.

**DATA-NOTATION-RULE-007:** Domain meanings must be expressed with named aliases and accompanying constraints:

```c
type RecordId = string;
type ItemIndex = uint32;
type DistanceMeters = float64;
type DurationMilliseconds = uint64;
```

**DATA-NOTATION-RULE-008:** The definition must state applicable ranges, units, indexing bases, normalization, precision, and validation rules. A type used across several specifications belongs in an appropriately categorized document under `data-model/`; types must be separated into multiple documents according to their subject when that improves ownership and navigation.

### Collections and semantic annotations

**DATA-NOTATION-RULE-009:** A repeated field must define whether order is significant, whether duplicates are permitted, whether an empty collection is valid, and any size limits.

**DATA-NOTATION-RULE-010:** Fixed-length arrays use C-style array syntax:

```c
struct Sha256Digest {
    required uint8 value[32];
}
```

Formal annotations express language-neutral semantics that may permit an implementation to select an optimized native representation:

```c
struct MetadataEntry {
    required string key;
    required string value;
}

struct RecordMetadata {
    @map(key_field = key)
    repeated MetadataEntry entries;
}

struct Selection {
    @set
    repeated RecordId record_ids;
}

struct Dimensions {
    @units(meters)
    @range(min = 0)
    required float64 width;
}
```

**DATA-NOTATION-RULE-011:** The recognized annotations are:

- `@map(key_field = <field>)`: the collection is logically keyed by the named field, keys are unique, and ordering is not significant unless separately stated;
- `@set`: values are unique and ordering is not significant;
- `@units(<unit>)`: numeric values use the named unit;
- `@range(min = <value>, max = <value>)`: values are constrained to the stated inclusive bounds; either bound may be omitted;
- `@identifier`: the value represents stable identity rather than arbitrary text or a number; and
- **DATA-NOTATION-RULE-012:** `@opaque`: consumers must not interpret the value's contents.

**DATA-NOTATION-RULE-013:** An implementation may use a language-specific optimized representation only when it preserves all specified semantics. Specifications must not use open-ended implementation annotations such as `@implementation_hint`, and must not prescribe language-specific optimizations.

**DATA-NOTATION-RULE-014:** Maps should be described as repeated entry structures with `@map` rather than by assuming that every target language has equivalent map behavior. If iteration order is semantically significant, it must be stated.

### Enumerations and tagged unions

**DATA-NOTATION-RULE-015:** Enumerations may declare an exact-width unsigned integer representation. A member without an explicit value receives the previous member's value plus one:

```c
enum OperationStatus : uint8 {
    pending = 0;
    completed;
    failed;
}
```

**DATA-NOTATION-RULE-016:** In this example, `completed` is `1` and `failed` is `2`. When an enum declares an underlying numeric type, the first member must have an explicit value. Every resolved value is normative, must be unique unless aliases are explicitly allowed, and must fit the declared underlying type.

**DATA-NOTATION-RULE-017:** Once an enumeration is accepted across an API, persistence, or compatibility boundary, its existing resolved values must not change. New implicitly numbered members should normally be appended. Removed numeric values must not be reused unless compatibility is explicitly irrelevant. The applicable specification must define how unknown values received across an external boundary are handled.

**DATA-NOTATION-RULE-018:** Raw C unions are prohibited. Variant data must use an explicit discriminator and tagged union so that exactly one active member can be identified.

### Translation into implementation languages

**DATA-NOTATION-RULE-019:** An implementation must use the closest target-language type that preserves the specified range, precision, signedness, cardinality, nullability, and collection semantics. Similar naming alone is insufficient. For example, a floating-point representation is insufficient for an integer type when it cannot exactly represent the full specified range.

**DATA-NOTATION-RULE-020:** Where a target language has no direct equivalent, the implementation must use validation, a wrapper type, or a suitable library rather than silently weakening the specified semantics.

**DATA-NOTATION-RULE-021:** For public APIs, Markdown notation is explanatory and must agree with the providing component's canonical machine-readable contract. It must not become a competing contract definition.
