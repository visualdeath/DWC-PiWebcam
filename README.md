# DWC-PiWebcam

![License](https://img.shields.io/github/license/visualdeath/DWC-PiWebcam?style=plastic) [![Release](https://img.shields.io/github/v/tag/visualdeath/DWC-PiWebcam?style=plastic)](https://github.com/visualdeath/DWC-PiWebcam/releases)

A Raspberry Pi webcam plugin for the Duet Web Control.  Allows real-time camera streaming, full screen with customizable overlays, and time lapse functions.

Forked from https://github.com/TLAS11/DWC-PiWebcam and updated to work with RepRap 3.3

This interface requires:

	a.	PiWebcam.zip from this repo's releases
	b.	RPi-Cam-Web-Interface
    
## Install Instructions:
1.  Install RPI-Cam-Web-Interface on the Raspberry Pi:  https://elinux.org/RPi-Cam-Web-Interface
2.  Install the zip file (PiWebcam.zip) using the Duet Web Control (upload it using Files > System)
3.  Enable the plugin under Settings > Machine-Specific > Machine-Specific Plugins
4.  Set your Webcam URL to http://<RPi-IP>/html/cam_pic_new.php?pDelay=40000

## Build instructions

1. Copy the contents from the `src` directory to the `src/plugins` directory of DWC
2. Append the following DwcPlugin definition to the default exports of `src/plugins/index.js`:
```
	new DwcPlugin({
		id: 'PiWebcam',
		name: 'Pi Webcam',
		author: 'VisualDeath',
		version,
		loadDwcResources: () => import(
			/* webpackChunkName: "PiWebcam" */
			'./PiWebcam/index.js'
		)
	}),
```
3. By performing this step, the plugin is registered as a built-in plugin. To test it, run `npm run serve` and activate it using the Settings -> General page
4. To build the final Webpack chunk, run `npm run build` and copy the resulting `PiWebcam` CSS files to `zip/dwc/css` and JS files to `zip/dwc/js`
5. Compress the files in the `zip` directory to a single file. The resulting bundle should be installable using the DWC plugin wizard
