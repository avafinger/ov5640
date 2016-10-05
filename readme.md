This is my modified OV5640 driver for the CMOS camera that incorporates many image resolutions and/or image quality. 
You can take advantage of a higher FPS, Image Quality (Preview or Capture) or Window size, choosing the one that best fit your needs.

This is expected to work with reasonable quality for some architectures like AW (32 bit and 64 bit).

Working window sizes and expected FPS (preview mode)

* QSXGA: 2592x1936 (7.5 FPS)
* QXGA: 2048x1536 (7.5 FPS)
* 1080P: 1920x1080 (7.5 FPS, 15 FPS)
* UXGA: 1600x1200 (7.5 FPS, 15 FPS)
* UXGA: 1280x960 (7.5 FPS, 15 FPS)
* 720P: 1280x720 (7.5 FPS, 15 FPS)
* XGA: 1024x768 (7.5 FPS, 15 FPS)
* SVGA: 800x600 (15 FPS, 30 FPS)
* VGA: 640x480 (15 FPS, 30 FPS)
* QVGA: 320x240 (30 FPS)
* QCIF: 176x144 (30 FPS with some artifacts)

Usage
=====
modprobe ov56405 frame_rate=2

where:

frame_rate=0 (default with no parameters), frame_rate=1 (7.5 FPS), frame_rate=2 (15 FPS), frame_rate=3 (30 FPS) (default=0 - or no parms - default settings)

default frame rate tries to use the best FPS possible with good quality. If you want better quality use frame_rate=1

Platform:
========

* (A64) BananaPi M64 / Pine64+ use: git clone -b A64 https://github.com/avafinger/ov5640
* (H3) OrangePi / BananaPi / NanoPi use: git clone -b Armbian_H3 https://github.com/avafinger/ov5640
* (A83T) BananaPi M3 will be ready soon

You can watch Armbian for the latest release / fix for this driver on H3 image.

Loading the OV5640 driver
=========================
	sudo modprobe ov5640 (or with frame_rate=2 [0,1,2,3]
	sudo modprobe vfe_v4l2


Application to grab frames - v4l2 / OpenCV
===========================================

	git clone https://github.com/avafinger/cap-v4l2
	cd cap-v4l2
	sudo ./install_deps.sh
	./build_script.sh
	./cap 1280 720 4 1 -999 -1 -1 (output will be frame_1280x720.jpg)

* you can also run a simple test ./test_ov5640.sh to grab all frames and display some FPS statistics

Important
=========

You need to load the correct driver (this latest ov5640) and make sure /dev/video0 is created.
Check if you have all dependencies.

Special thanks (no specific order):
----------------------------------
* Armbian (Igor / Thomas Kaiser / @mattday / @Gravelrash / @lvmc / @jules )- for the board (Xunlong) ,inspiration, information
* Nora Lee - Foxconn (for the boards and cameras)
* Yuefei - FriendlyArm (for the boards and cameras)
* linux-sunxi

History:
========

* ov5640 initial commit
* pass stability test (./test_ov5640.sh)
* Credits

