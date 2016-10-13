OV5640 with FriendlyArm Auto Focus Preview mode (Compile test only)
==================================================

This is my modified OV5640 driver with FA Auto Focus fix for the CMOS camera that incorporates many image resolutions and/or image quality.
You can take advantage of a higher FPS (Video Mode), Image Quality (Preview or Capture) or Window size, choosing the one that best fit your needs.

This is expected to work with reasonable quality H3

Working window sizes and expected FPS (video mode)
- QSXGA: 2592x1936 (7.5 FPS)
- QXGA: 2048x1536 (7.5 FPS)
- 1080P: 1920x1080 (7.5 FPS, 15 FPS)
- UXGA: 1600x1200 (7.5 FPS, 15 FPS)
- UXGA: 1280x960 (7.5 FPS, 15 FPS)
- 720P: 1280x720 (7.5 FPS, 15 FPS)
- XGA: 1024x768 (7.5 FPS, 15 FPS)
- SVGA: 800x600 (15 FPS, 30 FPS)
- VGA: 640x480 (15 FPS, 30 FPS)
- QVGA: 320x240 (30 FPS)
- QCIF: 176x144 (30 FPS with some artifacts)

Usage
=====
modprobe ov5640 (or with parameters: frame_rate=1)

where:

frame_rate=0 (default with no parameters = no parameters = best FPS / quality), frame_rate=1 (7.5 FPS), frame_rate=2 (15 FPS), frame_rate=3 (30 FPS) (default=0 - or no parms - default settings)

default frame rate tries to use the best FPS possible. If you want better quality use frame_rate=1

Application to grab frames - v4l2 / OpenCV
===========================================

	git clone https://github.com/avafinger/cap-v4l2
	cd cap-v4l2
	sudo ./install_deps.sh
	./build_script.sh
	./cap 1920 1080 4 1 -999 -1 -1 (output will be frame_1920x1080.jpg)

* you can also run a simple test ./test_ov5640.sh to grab all frames and display some FPS statistics



History Log:
* initial commit, compile test only (FIX ME)
* AF fix from FriendlyArm (need AF sensor) : https://github.com/friendlyarm/h3_lichee/commit/14973a798d79c08ce0dd68e2931356100bf01356 (need vfe.c changes)

FIX ME list
===========
- Sensor AF pinout check
- Activate AF on script.bin
- Preview mode and Image Mode
- vfe.c isp=1 & bayer=0 stability on load and unload driver
- testing AF with guvcview
