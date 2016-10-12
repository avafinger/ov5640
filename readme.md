OV5640 A83T - BananaPi M3 / Dual Camera (Experimental)
======================================================

This is my modified OV5640 driver for the CMOS camera that incorporates many image resolutions and/or image quality.
You can take advantage of a higher FPS (Video Mode), Image Quality (Preview or Capture) or Window size, choosing the one that best fit your needs.

This is expected to work with reasonable quality for most AW platform (32 bit and 64 bit)

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

Important
=========

You need to recompile the kernel with the new OV5640 driver and most important ** revert some BPI changes **
You need to load the correct driver (this latest ov5640) and make sure /dev/video0 is created.
Check if you have all dependencies.


History Log:
* initial commit, preparing for different boards and kernel versions
* Added default values
* Added output from cap
* A83T (dual camera)

Output from testing cap app
===========================

	TEST 0 - ( 2592 x 1936 )
	---- cap parameters -----
	width: 2592
	height: 1936
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 2592x1936 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453be0
	FPS[0]: 1.27
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453bf0
	FPS[1]: 7.51
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453c00
	FPS[2]: 7.51
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453c10
	FPS[3]: 7.51
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453be0
	FPS[4]: 7.50
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453bf0
	FPS[5]: 7.51
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453c00
	FPS[6]: 7.50
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453c10
	FPS[7]: 7.50
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453be0
	FPS[8]: 7.50
	Length: 7528448 	Bytesused: 7528448 	Address: 0x453bf0
	FPS[9]: 0.30
	------- Avg FPS: 7.51 --------
	
	TEST 1 - ( 2048 x 1536 )
	---- cap parameters -----
	width: 2048
	height: 1536
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 2048x1536 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453be0
	FPS[0]: 1.12
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453bf0
	FPS[1]: 7.51
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453c00
	FPS[2]: 7.51
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453c10
	FPS[3]: 7.50
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453be0
	FPS[4]: 7.50
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453bf0
	FPS[5]: 7.51
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453c00
	FPS[6]: 7.50
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453c10
	FPS[7]: 7.50
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453be0
	FPS[8]: 7.50
	Length: 4718592 	Bytesused: 4718592 	Address: 0x453bf0
	FPS[9]: 0.46
	------- Avg FPS: 7.51 --------
	
	TEST 2 - ( 1920 x 1080 )
	---- cap parameters -----
	width: 1920
	height: 1080
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 1920x1080 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453be0
	FPS[0]: 4.76
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453bf0
	FPS[1]: 12.52
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453c00
	FPS[2]: 12.50
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453c10
	FPS[3]: 12.50
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453be0
	FPS[4]: 12.49
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453bf0
	FPS[5]: 12.51
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453c00
	FPS[6]: 12.50
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453c10
	FPS[7]: 12.50
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453be0
	FPS[8]: 12.50
	Length: 3112960 	Bytesused: 3112960 	Address: 0x453bf0
	FPS[9]: 0.71
	------- Avg FPS: 12.50 --------
	
	TEST 3 - ( 1600 x 1200 )
	---- cap parameters -----
	width: 1600
	height: 1200
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 1600x1200 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453be0
	FPS[0]: 0.96
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453bf0
	FPS[1]: 7.51
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453c00
	FPS[2]: 7.50
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453c10
	FPS[3]: 7.51
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453be0
	FPS[4]: 7.50
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453bf0
	FPS[5]: 7.50
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453c00
	FPS[6]: 7.50
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453c10
	FPS[7]: 7.51
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453be0
	FPS[8]: 7.51
	Length: 2883584 	Bytesused: 2883584 	Address: 0x453bf0
	FPS[9]: 0.73
	------- Avg FPS: 7.51 --------
	
	TEST 4 - ( 1280 x 960 )
	---- cap parameters -----
	width: 1280
	height: 960
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 1280x960 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453be0
	FPS[0]: 6.77
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453bf0
	FPS[1]: 15.03
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453c00
	FPS[2]: 15.01
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453c10
	FPS[3]: 15.02
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453be0
	FPS[4]: 15.01
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453bf0
	FPS[5]: 15.01
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453c00
	FPS[6]: 15.01
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453c10
	FPS[7]: 15.01
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453be0
	FPS[8]: 15.01
	Length: 1843200 	Bytesused: 1843200 	Address: 0x453bf0
	FPS[9]: 1.15
	------- Avg FPS: 15.01 --------
	
	TEST 5 - ( 1280 x 720 )
	---- cap parameters -----
	width: 1280
	height: 720
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 1280x720 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453be0
	FPS[0]: 2.74
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453bf0
	FPS[1]: 32.99
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453c00
	FPS[2]: 32.87
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453c10
	FPS[3]: 32.87
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453be0
	FPS[4]: 32.87
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453bf0
	FPS[5]: 32.86
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453c00
	FPS[6]: 32.87
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453c10
	FPS[7]: 32.86
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453be0
	FPS[8]: 32.87
	Length: 1384448 	Bytesused: 1384448 	Address: 0x453bf0
	FPS[9]: 1.58
	------- Avg FPS: 32.88 --------
	
	TEST 6 - ( 1024 x 768 )
	---- cap parameters -----
	width: 1024
	height: 768
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 1024x768 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453be0
	FPS[0]: 1.25
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453bf0
	FPS[1]: 9.40
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453c00
	FPS[2]: 9.38
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453c10
	FPS[3]: 9.38
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453be0
	FPS[4]: 9.38
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453bf0
	FPS[5]: 9.38
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453c00
	FPS[6]: 9.38
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453c10
	FPS[7]: 9.38
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453be0
	FPS[8]: 9.39
	Length: 1179648 	Bytesused: 1179648 	Address: 0x453bf0
	FPS[9]: 1.63
	------- Avg FPS: 9.38 --------
	
	TEST 7 - ( 800 x 600 )
	---- cap parameters -----
	width: 800
	height: 600
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 800x600 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 720896 	Bytesused: 720896 	Address: 0x453be0
	FPS[0]: 2.16
	Length: 720896 	Bytesused: 720896 	Address: 0x453bf0
	FPS[1]: 22.57
	Length: 720896 	Bytesused: 720896 	Address: 0x453c00
	FPS[2]: 22.52
	Length: 720896 	Bytesused: 720896 	Address: 0x453c10
	FPS[3]: 22.52
	Length: 720896 	Bytesused: 720896 	Address: 0x453be0
	FPS[4]: 22.52
	Length: 720896 	Bytesused: 720896 	Address: 0x453bf0
	FPS[5]: 22.52
	Length: 720896 	Bytesused: 720896 	Address: 0x453c00
	FPS[6]: 22.52
	Length: 720896 	Bytesused: 720896 	Address: 0x453c10
	FPS[7]: 22.50
	Length: 720896 	Bytesused: 720896 	Address: 0x453be0
	FPS[8]: 22.53
	Length: 720896 	Bytesused: 720896 	Address: 0x453bf0
	FPS[9]: 2.79
	------- Avg FPS: 22.53 --------
	
	TEST 8 - ( 640 x 480 )
	---- cap parameters -----
	width: 640
	height: 480
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 640x480 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 462848 	Bytesused: 462848 	Address: 0x453be0
	FPS[0]: 3.28
	Length: 462848 	Bytesused: 462848 	Address: 0x453bf0
	FPS[1]: 30.12
	Length: 462848 	Bytesused: 462848 	Address: 0x453c00
	FPS[2]: 30.03
	Length: 462848 	Bytesused: 462848 	Address: 0x453c10
	FPS[3]: 30.03
	Length: 462848 	Bytesused: 462848 	Address: 0x453be0
	FPS[4]: 30.01
	Length: 462848 	Bytesused: 462848 	Address: 0x453bf0
	FPS[5]: 30.02
	Length: 462848 	Bytesused: 462848 	Address: 0x453c00
	FPS[6]: 30.07
	Length: 462848 	Bytesused: 462848 	Address: 0x453c10
	FPS[7]: 30.07
	Length: 462848 	Bytesused: 462848 	Address: 0x453be0
	FPS[8]: 30.03
	Length: 462848 	Bytesused: 462848 	Address: 0x453bf0
	FPS[9]: 4.14
	------- Avg FPS: 30.05 --------
	
	TEST 9 - ( 320 x 240 )
	---- cap parameters -----
	width: 320
	height: 240
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 320x240 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 118784 	Bytesused: 118784 	Address: 0x453be0
	FPS[0]: 3.20
	Length: 118784 	Bytesused: 118784 	Address: 0x453bf0
	FPS[1]: 30.15
	Length: 118784 	Bytesused: 118784 	Address: 0x453c00
	FPS[2]: 30.04
	Length: 118784 	Bytesused: 118784 	Address: 0x453c10
	FPS[3]: 30.02
	Length: 118784 	Bytesused: 118784 	Address: 0x453be0
	FPS[4]: 30.03
	Length: 118784 	Bytesused: 118784 	Address: 0x453bf0
	FPS[5]: 30.03
	Length: 118784 	Bytesused: 118784 	Address: 0x453c00
	FPS[6]: 30.03
	Length: 118784 	Bytesused: 118784 	Address: 0x453c10
	FPS[7]: 30.01
	Length: 118784 	Bytesused: 118784 	Address: 0x453be0
	FPS[8]: 30.04
	Length: 118784 	Bytesused: 118784 	Address: 0x453bf0
	FPS[9]: 9.92
	------- Avg FPS: 30.04 --------
	
	TEST 10 - ( 176 x 144 )
	---- cap parameters -----
	width: 176
	height: 144
	v4l2 buffers: 4
	exposure: -999
	hflip: -1
	sensor_vflip: -1
	Mode: V4L2_MODE_VIDEO
	Driver: "sunxi-vfe"
	Card: "sunxi-vfe"
	Bus: "sunxi_vfe vfe.12"
	Version: 1.0
	Capabilities: 05000001
	Input: 0
	V4L2 pixel formats:
	0: [0x50323234] '422P' (planar YUV 422)
	1: [0x32315559] 'YU12' (planar YUV 420)
	2: [0x32315659] 'YV12' (planar YVU 420)
	3: [0x3631564E] 'NV16' (planar YUV 422 UV combined)
	4: [0x3231564E] 'NV12' (planar YUV 420 UV combined)
	5: [0x3136564E] 'NV61' (planar YUV 422 VU combined)
	6: [0x3132564E] 'NV21' (planar YUV 420 VU combined)
	7: [0x32314D48] 'HM12' (MB YUV420)
	8: [0x56595559] 'YUYV' (YUV422 YUYV)
	9: [0x55595659] 'YVYU' (YUV422 YVYU)
	10: [0x59565955] 'UYVY' (YUV422 UYVY)
	11: [0x59555956] 'VYUY' (YUV422 VYUY)
	12: [0x31384142] 'BA81' (RAW Bayer BGGR 8bit)
	13: [0x47524247] 'GBRG' (RAW Bayer GBRG 8bit)
	14: [0x47425247] 'GRBG' (RAW Bayer GRBG 8bit)
	15: [0x47425247] 'GRBG' (RAW Bayer RGGB 8bit)
	16: [0x30314742] 'BG10' (RAW Bayer BGGR 10bit)
	17: [0x30314247] 'GB10' (RAW Bayer GBRG 10bit)
	18: [0x30314142] 'BA10' (RAW Bayer GRBG 10bit)
	19: [0x30314142] 'BA10' (RAW Bayer RGGB 10bit)
	20: [0x32314742] 'BG12' (RAW Bayer BGGR 12bit)
	21: [0x32314247] 'GB12' (RAW Bayer GBRG 12bit)
	22: [0x32314142] 'BA12' (RAW Bayer GRBG 12bit)
	23: [0x32314142] 'BA12' (RAW Bayer RGGB 12bit)
	
	Sensor size: 176x144 pixels
	Pixel Format: V4L2_PIX_FMT_YUV420
	Frame #10 will be saved!
	Length: 40960 	Bytesused: 40960 	Address: 0x453be0
	FPS[0]: 3.23
	Length: 40960 	Bytesused: 40960 	Address: 0x453bf0
	FPS[1]: 30.13
	Length: 40960 	Bytesused: 40960 	Address: 0x453c00
	FPS[2]: 30.04
	Length: 40960 	Bytesused: 40960 	Address: 0x453c10
	FPS[3]: 30.03
	Length: 40960 	Bytesused: 40960 	Address: 0x453be0
	FPS[4]: 30.03
	Length: 40960 	Bytesused: 40960 	Address: 0x453bf0
	FPS[5]: 30.03
	Length: 40960 	Bytesused: 40960 	Address: 0x453c00
	FPS[6]: 30.03
	Length: 40960 	Bytesused: 40960 	Address: 0x453c10
	FPS[7]: 30.03
	Length: 40960 	Bytesused: 40960 	Address: 0x453be0
	FPS[8]: 30.03
	Length: 40960 	Bytesused: 40960 	Address: 0x453bf0
	FPS[9]: 13.27
	------- Avg FPS: 30.04 --------

