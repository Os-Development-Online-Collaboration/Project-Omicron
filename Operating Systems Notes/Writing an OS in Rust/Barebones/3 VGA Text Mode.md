### Format macros

```rust
format!      // described above
write!       // first argument is either a &mut io::Write or a &mut fmt::Write, the destination
writeln!     // same as write but appends a newline
print!       // the format string is printed to the standard output
println!     // same as print but appends a newline
eprint!      // the format string is printed to the standard error
eprintln!    // same as eprint but appends a newline
format_args! // described below.
```

### VGA Text Buffer

Accessible via [memory-mapped I/O](https://en.wikipedia.org/wiki/Memory-mapped_I/O) to the address `0xb8000`

| Bit(s) | Value            |
| ------ | ---------------- |
| 0-7    | ASCII code point |
| 8-11   | Foreground color |
| 12-14  | Background color |
| 15     | Blink            |
-> First byte represents *which* character should be printed

| Number | Color      | Number + Bright Bit | Bright Color |
| ------ | ---------- | ------------------- | ------------ |
| 0x0    | Black      | 0x8                 | Dark Gray    |
| 0x1    | Blue       | 0x9                 | Light Blue   |
| 0x2    | Green      | 0xa                 | Light Green  |
| 0x3    | Cyan       | 0xb                 | Light Cyan   |
| 0x4    | Red        | 0xc                 | Light Red    |
| 0x5    | Magenta    | 0xd                 | Pink         |
| 0x6    | Brown      | 0xe                 | Yellow       |
| 0x7    | Light Gray | 0xf                 | White        |
-> Second byte represents *how* the character should be printed

### Code Page 437
Character set including all ASCII characters, with some additional ones

![](https://upload.wikimedia.org/wikipedia/commons/f/f8/Codepage-437.png)



