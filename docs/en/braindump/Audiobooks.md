
# Download Audible file (aax)
- https://www.audible.ca/library/titles

# Extract "activation_bytes"
## Get Checksum
```bash
$ ffprobe <filename>.aax  2>&1 | grep checksum

[mov,mp4,m4a,3gp,3g2,mj2 @ 0x1dde580] [aax] file checksum == 999a6ab8...
```

## Extract activation_bytes
```bash
$ git clone https://github.com/inAudible-NG/tables.git
$ cd tables
$ ./rcrack . -h 999a6ab8...
statistics
-------------------------------------------------------
plaintext found:                              1 of 1
total time:                                   13.98 s
...
result
-------------------------------------------------------
999a6ab8...                               xyz   hex:CAFED00D
```
"activation_bytes" is CAFED00D here.

# Convert aax to mp3
```bash
$ ffmpeg -activation_bytes XXXX -i audiobook.aax audiobook.mp3
```

# Reference
- [How to Break Audible DRM](https://kylepiira.com/2019/05/12/how-to-break-audible-drm/)
- [Activation Key](https://github.com/inAudible-NG/tables)
