
# Rpi WebRTC Streamer Package

This Repo is for testing the deb package of rpi-webrtc-streamer. For more information on rpi-webrtc-streamer, please refer to this [Rpi-WebRTC-Streamer Repo](https://github.com/kclyu/rpi-webrtc-streamer).

## Supported Hardware

### Raspberry PI 
- Raspberry PI 2/3
- Raspberry Pi Zero/Zero W (ZeroW tested)

### Video Camera
- RPI Camera board V1/V2
- Arducam 5 Megapixels 1080p Sensor OV5647 Mini Camera Video Module

## Latest Deb Package
The latest Deb versions are listed below.


|Deb File|SHA256sum|
|----------------|---------------|
|[rws_0.65.0_armhf.deb](https://github.com/kclyu/rpi-webrtc-streamer-deb/blob/master/rws_0.65.0_armhf.deb)|46ef8828cefcd834be773d12a46071caa683f7f1ba24a2634bbee0d2c5add567|
[rws_0.65.0_RaspiZeroW_armhf.deb](https://github.com/kclyu/rpi-webrtc-streamer-deb/blob/master/rws_0.65.0_armhf.deb)|dbecc32f6f1b857897c03da067a661bf536092385a91439fc175414d9f37dc5e|

## Downloading Deb Package

The downloaded file can be installed with the following command.

*The two apt commands below does not need to be run if the current Raspberry PI OS is up to date.*
```
sudo apt update
sudo apt full-upgrade

sudo dpkg -i rws_xxx_armhf.deb
```

To remove rws package, please use following command
```
sudo dpkg -r rws
```
*Since the current log directory is located in the installation directory, you can delete the '/opt/rws' directory manally after dpkg remove.*
##  Installation Directory
When the installation is complete, the following files and directories are created under **/opt/rws**.

|File/Directory|Description|
|---------------|------------|
|LICENSE|There are LICENSE files for the S/W package and libraries used by RWS.|
|webrtc-streamer|RWS man binary executable|
|etc|configuration files|
|web-root|Where test html files and js files are located.|
|log|Directory where log messages are stored. Files from rws_log_0 to rws_log_9 are created. If webrtc-streamer is not restarted, the files will not moved between shift folders. When the process is restarted, the log files in the '/opt/rws/log' directory are moved to 00. And files in 00 move to 01, 01 move to 02 ... the log files in the last 09 directory are deleted.|

##  Process Management 
RWS is only compatible with systemd. To execute the process and check the status, use the following command.

#### Start
```
sudo systemctl start rws
```
#### Stop
```
sudo systemctl stop rws
```
#### Status/Monitoring
`sudo systemctl status rws` is used for process status checking.
`sudo journalctl -u rws` for  log message for process start/stop/standard error log checking.
```
sudo systemctl status rws
● rws.service - Rpi WebRTC Streamer
   Loaded: loaded (/etc/systemd/system/rws.service; enabled)
   Active: active (running) since Thu 2017-06-08 21:08:45 KST; 2h 47min ago
 Main PID: 14968 (webrtc-streamer)
   CGroup: /system.slice/rws.service
           └─14968 /opt/rws/webrtc-streamer --log /opt/rws/log

Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib pcm.c:2239:(snd_pcm_open_noupdate) Unknown PCM
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib pcm.c:2239:(snd_pcm_open_noupdate) Unknown PCM
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib pcm.c:2239:(snd_pcm_open_noupdate) Unknown PCM
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 22:04:44 raspberrypi webrtc-streamer[14968]: ALSA lib pcm.c:2239:(snd_pcm_open_noupdate) Unknown PCM
Hint: Some lines were ellipsized, use -l to show in full.

sudo journalctl -u rws
Jun 08 19:56:05 raspberrypi systemd[1]: Stopped Rpi WebRTC Streamer.
Jun 08 19:56:05 raspberrypi systemd[1]: Stopped Rpi WebRTC Streamer.
Jun 08 21:08:45 raspberrypi systemd[1]: Starting Rpi WebRTC Streamer...
Jun 08 21:08:45 raspberrypi systemd[1]: Started Rpi WebRTC Streamer.
Jun 08 21:08:45 raspberrypi systemd[1]: Started Rpi WebRTC Streamer.
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib pcm.c:2239:(snd_pcm_open_noupdate) Unknown PCM
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib pcm.c:2239:(snd_pcm_open_noupdate) Unknown PCM
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib control.c:953:(snd_ctl_open_noupdate) Invalid CTL
Jun 08 21:09:18 raspberrypi webrtc-streamer[14968]: ALSA lib pcm.c:2239:(snd_pcm_open_noupdate) Unknown PCM
```
#### Open Testing URL in Chrome Browser
Open the following URL in the chrome browser will display the native-peerconnection testing page.

```
http://your-private-ip-address:8889/native-peerconnection/
```
*`8889` port number is the websocket_port specified in the config file, and the URL protocol uses http instead of https.*


## Version History
Please refer to RWS repo for version-specific history and function description.


 

