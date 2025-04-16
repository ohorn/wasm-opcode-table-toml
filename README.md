# WebAssembly Opcode Table (TOML)

This repository contains a structured reference of the WebAssembly instruction set and its opcodes, formatted as a [TOML](https://toml.io) file.

## Overview

The [instructions.toml]() file lists all instructions as an array-of-tables under the key `[[instructions]]`.

Each entry represents a single instruction (or more precisely, a single opcode) and includes details such as its name, category, binary opcode, immediate arguments, and stack signature.

| Key          | Type              | Value                                                                     |
| ------------ | ----------------- | ------------------------------------------------------------------------- |
| `name`       | string            | The name of the instruction.                                              |
| `variant`    | string (optional) | A unique identifier for a specific variant of the instruction, if needed. |
| `opcode`     | number or array   | The binary opcode for the instruction.                                    |
| `category`   | string            | The category of the instruction as defined in the spec.                   |
| `immediates` | array (optional)  | The immediate arguments, if any.                                          |
| `stack-type` | table (optional)  | The instruction type, describing stack input and output types.            |
| `feature`    | string (optional) | The feature proposal to which the instruction belongs, if any.            |
| `since`      | string (optional) | The first major version of WebAssembly that includes the instruction.     |

## Examples

```toml
[[instructions]]
name = "i32.add"
opcode = 0x6A
category = "numeric"
stack-type = { from = [ { type = "i32" }, { type = "i32" } ], to = [ { type = "i32" } ] }
since = "1"
```

```toml
[[instructions]]
name = "table.fill"
opcode = [0xFC, 17]
category = "table"
immediates = [ { type = "tableidx", name = "x" } ]
stack-type = { from = [ { type = "i32" }, { type-of = "x" }, { type = "i32" } ], to = [] }
feature = "reference-types"
since = "2"
```
