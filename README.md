# memcached-rs

[![Build Status](https://travis-ci.org/zonyitoo/memcached-rs.svg)](https://travis-ci.org/zonyitoo/memcached-rs)

Memcached library in Rust

## Usage

```rust
extern crate memcached;

use memcached::client::Client;
use memcached::proto::{Operation, Binary};

fn main() {
    let mut client = Client::connect([("127.0.0.1", 11211, Binary, 1)]);

    client.set(b"Foo", b"Bar", 0xdeadbeef, 2).unwrap();

    let (value, flags) = client.get(b"Foo").unwrap();

    assert_eq!(value.as_slice(), b"Bar");
    assert_eq!(flags, 0xdeadbeef);
}
```