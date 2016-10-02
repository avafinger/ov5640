OV5640 for Armbian H3 (Experimental)
====================================

This is my modified OV5640 driver for the CMOS camera that incorporates many image resolutions and/or image quality.
You can take advantage of a higher FPS, Image Quality (Preview or Capture) or Window size, choosing the one that best fit your needs.

This is expected to work with reasonable quality for some architectures like AW (H3 / A20)

Working window sizes and expected FPS (preview mode)
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
modprobe ov5640 frame_rate=2

where:

frame_rate=0 (default with no parameters), frame_rate=1 (7.5 FPS), frame_rate=2 (15 FPS), frame_rate=3 (30 FPS) (default=0 - or no parms - default settings)

History Log:
* initial commit, preparing for the different boards and kernel version
* Armbian kernel 3.4.102 - Compiling test only
* Armbian kernel 3.4.112 - Fixed HFLip on some window sizes (re-done)
* Fix stabilty