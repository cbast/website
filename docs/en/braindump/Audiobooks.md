
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
ffmpeg -activation_bytes XXXX -i audiobook.aax audiobook.mp3
```

# Convert to chapters
Extract chapters info:
```bash
ffprobe -i <filename.aax> -print_format json -show_chapters  2>&1 > chapters.json
```

Convert aax to mp3s
```bash
#!/bin/bash
# Description: Split an 
# Requires: ffmpeg, jq
# Author: Hasan Arous
# License: MIT

in="$1"
out="$2"
splits=""
while read start end title; do
  splits="$splits -c copy -ss $start -to $end $out/$title.mp3"
done <<<$(cat chapters.json \
  | jq -r '.chapters[] | .start_time + " " + .end_time + " " + (.tags.title | sub(" "; "_"))')

ffmpeg  -i "$in" $splits
```

# Set MP3 tags
```bash
#!/bin/bash
# Description: Split an 
# Requires: ffmpeg, jq
# Author: Hasan Arous
# License: MIT

in="$1"
out="$2"


ARTIST=$(ffprobe -i "${in}" -show_entries format_tags=artist -of json | jq -r '.format.tags.artist')
TITLE=$(ffprobe -i "${in}" -show_entries format_tags=title -of json | jq -r '.format.tags.title')
echo "ARTIST = ${ARTIST}"
echo "TITLE = ${TITLE}"

while read track title; do
	echo "track=${track}"
	#id3v2 -T "${track}"-t "${title}" -a "${ARTIST}" -A "${TITLE}" ${out}/${title}.mp3
done <<<$(ffprobe -i "$in" -print_format json -show_chapters \
	| jq -r  '.chapters[] | {id, "title": (.tags.title | sub(" "; "_"))} | join(" ")')
```

# Reference
- [How to Break Audible DRM](https://kylepiira.com/2019/05/12/how-to-break-audible-drm/)
- [Activation Key](https://github.com/inAudible-NG/tables)
- [StackOverflow - Using ffmpeg to split an Audible audio-book into chapters](https://unix.stackexchange.com/a/612124)
