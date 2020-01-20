# Media samples for testing podcast transcoding

Video and audio samples of both me saying *Kim Kardashian* (multiple short samples), and a snippet of Richard Nixon's resignation speech (a single long sample). Used for [Media Cloud's](https://github.com/berkmancenter/mediacloud) podcast transcription testing.

Stored here in order to not litter the main repo with huge media files


## Creation process

1. Shoot video with *QuickTime Player*, save it as `kim_kardashian.mov`.
2. Rescale initial video to 480p:

    ```shell
    ffmpeg -i kim_kardashian.mov -s 640x360 -c:a copy kim_kardashian-prores-pcm_s24be.mov
    rm kim_kardashian.mov
    ```


### PCM 16 bit

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -vn -acodec pcm_s16le kim_kardashian-linear16.wav
```

### FLAC 24 bit

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -vn -acodec flac kim_kardashian-flac24.flac
```

### FLAC 16 bit

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -vn -acodec flac -sample_fmt s16 kim_kardashian-flac16.flac
```


### MU-LAW

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -vn -acodec pcm_mulaw kim_kardashian-mulaw.wav
```


### Opus in Ogg container

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -vn -acodec libopus kim_kardashian-opus.opus
```


### MP3 (stereo)

```
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -vn -acodec mp3 kim_kardashian-mp3-stereo.mp3
```


### MP3 (mono)

```
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -vn -acodec mp3 -ac 1 kim_kardashian-mp3-mono.mp3
```


### AAC in MP4 container

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -vn -acodec aac kim_kardashian-aac.m4a
```


### MKV with two (MP3, AAC) audio channels

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -map 0:0 -map 0:1 -map 0:1 -c:v libx264 -c:a:0 aac -c:a:1 mp3 kim_kardashian-h264-aac-mp3.mkv
```


### MKV with no audio

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -c:v libx264 -an kim_kardashian-h264-noaudio.mkv
```


### Invalid media file

```shell
dd if=/dev/urandom of=kim_kardashian-invalid.mp3 bs=1k count=60
```


### Nixon resignation speech

Useful for testing longer transcription operations, i.e. what happens if we submit a job and try to fetch its results too soon.

```shell
curl --output nixon_speech-vorbis-15m22s.ogg \
    https://upload.wikimedia.org/wikipedia/commons/e/e6/Nixon_resignation_audio_with_buzz_removed.ogg
ffmpeg -i nixon_speech-vorbis-15m22s.ogg -t 60 -acodec copy nixon_speech-vorbis-1m.ogg
rm nixon_speech-vorbis-15m22s.ogg
```


## License

I thereby disclaim any copyright of these media files of me saying *Kim Kardashian*, therefore they are in public domain. [Nixon speech](https://en.wikipedia.org/wiki/File:Nixon_resignation_audio_with_buzz_removed.ogg) is in public domain.

