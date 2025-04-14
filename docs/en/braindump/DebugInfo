# Split debug info
Compile binary in debug mode, then split the debug info as a separate file.

The `Build.Id` will remain the same after the operation, ensuring traceability.

```bash
# Compile binary with -g
gcc -o foo -g main.c
file foo
# foo: ..., ..., ..., ..., interpreter /lib/ld-linux-aarch64.so.1, BuildID[sha1]=XYZ, with debug_info, not stripped

# Split Debug Info
objcopy --only-keep-debug foo foo.debug # Copy debug info from foo to foo.debug
strip -g foo # Remove foo's debug info

file foo
# foo: ..., ..., ..., ..., interpreter /lib/ld-linux-aarch64.so.1, BuildID[sha1]=XYZ, not stripped

file foo.debug
# foo: ..., ..., ..., ..., interpreter *empty*, BuildID[sha1]=XYZ, with debug_info, not stripped
```

# Re-Assemble debug info
```bash
objcopy --add-gnu-debuglink=foo.debug foo

file foo
# foo: ..., ..., ..., ..., interpreter /lib/ld-linux-aarch64.so.1, BuildID[sha1]=XYZ, with debug_info, not stripped
```

# References
- [sourceware - Debugging Information in Separate Files](https://sourceware.org/gdb/current/onlinedocs/gdb.html/Separate-Debug-Files.html)
