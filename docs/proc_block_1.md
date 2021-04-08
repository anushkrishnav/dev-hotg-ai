---
title: Components of a Processing Block
sidebar_label: Components of a Processing Block
---

Processing Blocks are used to pre- and post- process data.

A barebones file structure for a processing block can be generated with the following cargo command:

```rust
cargo new `proc_block_name` --lib
```

The following file will be generated:

```bash
.
├── Cargo.toml
└── src
    └── lib.rs
```

Each processing block has 2 components

- `lib.rs` file, where the logic of the processing block is written
- `Cargo.toml` file, which contains package information and dependencies

## Dependencies

Processing blocks are dependent on the runic_types library. This can be added to the Cargo.toml file in the processing block.

```rust
[dependencies]
runic-types = { path = "../../runic-types" }
```

## Logic

The `lib.rs` should contain the following components.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;1. `no_std` environment
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2. `runic_types::Transform` module
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;3. struct
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;4. Transform method

Processing Blocks are implemented as structs with a transform method hence 3. and 4. are necessary components.

```rust
#![no_std]

use runic_types::Transform;

pub struct ProcBlock<T> {
    genericParameter: T,
}

impl<T> Transform<T> for ProcBlock<T>{
    type Output = /* Output of the ProcBlock (Should match the Runefile Output)*/;
    fn transform(&mut self, input: /*Input of function*/) -> Self::Output {
        // Logic goes here
    }
}
```

Our next tutorial will explore the creation of a Processing Block in greater detail.
