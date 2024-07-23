DaVinci doesn't support AAC audio, it's easiest to re-encode it using FFmpeg to use PCM. Here's an example on Linux:
```
ffmpeg -i input.mp4 -c:v copy -c:a pcm_s16le fixed_output.mkv
```
The output will have audio when imported into DaVinci Resolve.