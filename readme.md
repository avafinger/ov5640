OV5640 (Experimental)
=====================

This is my modified OV5640 driver for the CMOS camera that incorporates many image resolutions and/or image quality.
You can take advantage of a higher FPS, Image Quality (Preview or Capture) or Window size, choosing the one that best fit your needs.

This is expected to work with reasonable quality for some architectures like AW (32 bit and 64 bit), nexell and possibly Actions. 

Working window sizes and expected FPS (preview mode)

Usage
=====
modprobe ov56405 frame_rate=2

where:

frame_rate=0 (7.5 FPS), frame_rate=1 (15 FPS), frame_rate=2 (30 FPS) (default=0 - 7.5 FPS)

History Log:
* initial commit, preparing for the different boards and kernel version

