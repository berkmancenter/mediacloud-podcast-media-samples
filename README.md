# Media samples for testing podcast transcoding

Video and audio samples of me saying *Kim Kardashian*. Used for [Media Cloud's](https://github.com/berkmancenter/mediacloud) podcast transcription testing.

Stored here for the huge binary fines not to litter the main repo.


## Creation process

1. Shoot video with *QuickTime Player*, save it as `kim_kardashian.mov`.
2. Rescale initial video to 480p:

    ```shell
    ffmpeg -i kim_kardashian.mov -s 640x360 -c:a copy kim_kardashian-prores-pcm_s24be.mov
    ```


### PCM 16 bit

```shell
ffmpeg -i kim_kardashian.mov -vn -acodec pcm_s16le kim_kardashian-linear16.wav
```

### FLAC 24 bit

```shell
ffmpeg -i kim_kardashian.mov -vn -acodec flac kim_kardashian-flac24.flac
```

### FLAC 16 bit

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be.mov -vn -acodec flac -sample_fmt s16 kim_kardashian-flac16.flac
```


### MU-LAW

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be.mov -vn -acodec pcm_mulaw kim_kardashian-mulaw.wav
```


### Opus in Ogg container

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be.mov -vn -acodec libopus kim_kardashian-opus.opus
```


### MP3

```
ffmpeg -i kim_kardashian-prores-pcm_s24be.mov -vn -acodec mp3 kim_kardashian-mp3.mp3
```


### AAC in MP4 container

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be.mov -vn -acodec aac kim_kardashian-aac.m4a
```


### MKV with two (MP3, AAC) audio channels

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -map 0:0 -map 0:1 -map 0:1 -c:v libx264 -c:a:0 aac -c:a:1 mp3 kim_kardashian-h264-aac-mp3.mkv
```


### MKV with no audio

```shell
ffmpeg -i kim_kardashian-prores-pcm_s24be-480p.mov -c:v libx264 -an kim_kardashian-h264-noaudio.mkv
```


## License

I thereby disclaim any copyright of these media files of me saying *Kim Kardashian*, therefore they are in public domain.
