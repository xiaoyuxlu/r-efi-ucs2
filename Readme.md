# EFI-UCS2

UCS-2 encoding and decoding library.

## Background

This crate is for RustPkg [edkii-rust](https://github.com/jyao1/edk2/tree/edkii-rust)

EFI use UCS2 as default string type. But string type in rust is UTF8.
So we create this library for encoding string.

## Example

```rust
    use efi_ucs2::*;

    let input = "中国";
    let mut buffer = [0u16; 2];
    assert_eq!(encode(input, &mut buffer).is_ok(), true);
    assert_eq!(buffer[0], 0x4e2du16);
    assert_eq!(buffer[1], 0x56fdu16);

    let mut u8_buffer = [0u8; 6];
    let u16_str = [0x4e2du16, 0x56fdu16]; // 中国
    let len = decode(&u16_str, &mut u8_buffer).unwrap_or(0);
    assert_eq!(len, 6);
    assert_eq!(core::str::from_utf8(&u8_buffer[..]), Ok("中国"));
```

## License

[MIT License](https://spdx.org/licenses/MIT.html)