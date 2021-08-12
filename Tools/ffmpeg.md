# FFMPEG

***
## Cut videos

    ffmpeg -noaccurate_seek -ss 00:00:45.0 -i [input] -to 00:02:00.0 -c copy output.mp4
    ffmpeg -noaccurate_seek -ss 00:00:00.0 -i 24.mp4 -to 00:00:47.0 -c copy output.mp4
    ffmpeg -noaccurate_seek -ss 00:00:00.0 -i a.mkv -to 00:39:11.0 -c copy output.mkv


***
## Merge videos (super fast)

    echo file file1.mp4 >  mylist.txt
    echo file file2.mp4 >> mylist.txt
    echo file file3.mp4 >> mylist.txt
    ffmpeg -f concat -i mylist.txt -c copy out.mp4


***
## change volume

    ffmpeg -i out.mp4 -filter:a "volume=2" out_.mp4
    ffmpeg -i mus.mp4 -filter:a "volume=0.2" mus_.mp4


***
## Merge audio

    ffmpeg -filter_complex "amovie=file1.mp3 [a0]; amovie=file2.mp3 [a1]; [a0][a1] amix=inputs=2:duration=shortest [aout]" -map [aout] -acodec mp3 file_merged.mp3



***
## Replace audio

    ffmpeg -i 1.mp4 -i 1.mp3 -c:v copy -map 0:v:0 -map 1:a:0 out.mp4

    ffmpeg -i "out.mp4" -i "out.mp3" -shortest outPutFile.mp4


***
## FFMPEG merge audio with video with audio

    ffmpeg -i out.mp4 -i mus.mp4  -filter_complex \
    "[1:a]volume=enable='between(t,27,33)+between(t,38,42)'[1a];[0:a][1a]amerge=inputs=2[a]" \
    -map 0:v -map "[a]" -c:v copy -c:a aac -ac 2 -shortest out_.mp4


***
## Map audio to mono
Simple fix videos with out of phase in stereo

    ffmpeg -i 1.mp4 -map_channel 0.1.0 -c:v copy mono.mp4


***
## Config mic input to record mono
Mic is recording stereo out of phase and gets canceled when a device ouputs mono

    pacmd list-sources|grep -e name:
        alsa_input.pci-0000_00_1f.3.analog-stereo

    pacmd load-module module-remap-source master=alsa_input.pci-0000_00_1f.3.analog-stereo master_channel_map=front-left channel_map=mono

Undo changes

    pacmd unload-module module-remap-source

Merge stereo to mono and generate cancellation --> usefull to test the problem
in https://trac.ffmpeg.org/wiki/AudioChannelManipulation

    ffmpeg -i stereo.mp4 -ac 1 mono.mp4


***
## Merge videos with Mencoder:
Both videos must have equal dimensions, height x width, works fine with screen captures from simple-screen-recorder (with the same screen size)

    mencoder -oac mp3lame -ovc x264 1.mp4 2.mp4 -o suma.mp4
