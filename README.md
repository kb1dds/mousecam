# mousecam

Raspberry PI utilities for continuously monitoring the mice that enter our house.

## Installation instructions

1. Install Rasberry PI OS, using the default tools to select a hostname
2. You might find it useful to configure your Wifi router to issue a static IP.  That makes access later easier
3. Copy the `security_camera` script to `/home/pi/`
4. Run the following:
```
$ sudo apt install ffmpeg openssh-server
$ chmod u+x security_camera
```
5. Configure `crontab` to run the camera on boot.  Run the command
```
$ crontab -e
```
and then add the line:
```
@reboot /home/pi/security_camera >/dev/null 2>&1
```
6. Reboot the Pi.  Everything should be running at this point; you can check this by ssh'ing into the Pi as user `pi`.

## Default behavior

You should see files `video_*.avi` filling up in `/home/pi/`.

The default settings in `security_camera` yield files that contain one hour of video at 5 frames per second.  The videos are numbered sequentially and will overwrite after one week.  This fits within a single 32 GB memory card.

Timestamps are placed on the upper-left corner of the video frame.

It is not generally a good idea to play the videos on the Pi as this loads the network and the Pi.  Instead, copy the desired video files to another machine for inspection (use `scp` with regexes for file names).  The `vlc` player works well.

The `motion_detect` script will detect motion on every AVI file in a directory.  This is helpful if the mice visit infrequently.  This script uses `dvr-scan`: [https://github.com/Breakthrough/DVR-Scan].