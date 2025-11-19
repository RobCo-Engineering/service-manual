# Creating Music Files

This tutorial will guide you through the process of creating music files
compatible with the Pip-Boy 3000 Mk V Media Converter.

## Index

- ## [Pip-Boy 3000 Mk V Audio Conversion](#pip-boy-3000-mk-v-audio-conversion)
  - [Manually Using FFmpeg](#manually-using-ffmpeg)

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

## Pip-Boy 3000 Mk V Audio Conversion <a name="pip-boy-3000-mk-v-audio-conversion"></a>

### Using the Pip-Boy 3000 Mk V Media Converter <a name="using-the-pip-boy-3000-mk-v-media-converter"></a>

1. Download the [Pip-Boy 3000 Mk V Media
   Converter][link-pip-boy-media-converter] from the [releases
   page][link-pip-boy-media-converter-releases].

2. Follow the instructions in the repository to convert your audio files to the
   correct format for the Pip-Boy 3000 Mk V.

### Manually Using FFmpeg (Pip-Boy 3000 Mk V) <a name="manually-using-ffmpeg"></a>

1. Install [FFmpeg][link-ffmpeg]

2. Open a terminal window in the same directory as your audio file.

3. Run the following command, replacing `input.mp3` with the name of your audio
   file and `output.wav` with your desired output file name.

```bash
ffmpeg -i "input.mp3" -ac 1 -ar 16000 -sample_fmt s16 -c:a pcm_s16le -f wav output.wav
```

Your output is cusomizable, heres a few common examples:

- `volume=10dB` - Increase volume by 10 decibels, useful for quiet audio

```bash
ffmpeg -i "input.mp3" -ac 1 -ar 16000 -af "volume=10dB" -sample_fmt s16 -c:a pcm_s16le -f wav output.wav
```

- `atempo=1.25` - Speed up audio by 25%

```bash
ffmpeg -i "input.mp3" -ac 1 -ar 16000 -af "atempo=1.25" -sample_fmt s16 -c:a pcm_s16le -f wav output.wav
```

See the full list here: https://ffmpeg.org/ffmpeg-filters.html

<p align="right">[ <a href="#index">Index</a> ]</p>

<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->
<!---------------------------------------------------------------------------->

[link-ffmpeg]: https://ffmpeg.org/download.html
[link-pip-boy-media-converter]:
  https://github.com/CodyTolene/pip-boy-3000-mk-v-media-converter
[link-pip-boy-media-converter-releases]:
  https://github.com/CodyTolene/pip-boy-3000-mk-v-media-converter/releases
