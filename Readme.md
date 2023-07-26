# CITIC-MTMC dataset

This repository contains the CITIC-MTMC dataset. A multi-target multi-camera video dataset for indoor location and tracking of people.

The recordings were carried out inside the CITIC research center. Five cameras were deployed in four spaces of the building: an entrance hall with two cameras (*HallWide*, *HallSeg*), two passageways with one camera each (*PF* and *PC*), and a showroom with one camera (*Showroom*).

### Ground-truth obtention

A system based on discrete waypoints was established to obtain the ground-truth positions of each person during the capture. These waypoints were graphic marks placed on the building floor at predetermined and known positions. Each person carries a smartphone with an application that sends a notification to a server when the person is just above one of these waypoints.

The mobile application also integrates a BLE beacon scanner. This scanner detects the signal level (RSS) and the identifiers (UUID, major, and minor of the iBeacon format) of each nearby BLE beacon. This data is sent to the server continuously, adding a timestamp to each message. This optional feature allows to assess the BLE location accuracy against other technologies, or to improve the tracking results by using this additional information.

The source code of the server and the mobile application is available at the following repositories:

 - [Backend](https://github.com/GTEC-UDC/checkpoint-manager-backend)
 - [Admin](https://github.com/GTEC-UDC/checkpoint-manager-admin)
 - [Mobile application](https://github.com/GTEC-UDC/CheckpointManagerNative) for iOS and android.


### Hardware setup

The camera model, resolution, and maximum FPS used to record the video streams are:

 - *PF* and *PC*: ieGeek IG20. 1920x1080. 12.5 FPS.
 - *Showroom* and *HallWide*: Dahua DH-SD22204T-GN. 1280x720. 10 FPS.
 - *HallSeg*: AXIS M5525-E. 720x576. 25 FPS.

The camera recordings were processed to have a fixed frame-rate of 25 FPS. This was necessary because the cameras stored the video streams with a variable frame-rate, reducing the frame-rate when no motion was detected to improve the compression rate. Lens distortion was also corrected using the [Defish0r plugin](https://frei0r.dyne.org/) to remove the fisheye lens effect.

In addition to the camera setup, we also deployed eight BLE beacons to measure the proximity of individuals to them. Specifically, we used the Sevenix Postrum TWF535-BR2 beacons, which utilize the Panasonic PAN1721 BLE module.
Three  different smartphones were used to measure the RSS from the BLE beacons: an iPhone 11 Pro, a Google Pixel 4, and a POCO F3.


### Provided files

The video recordings are located in capture1, capture2, and capture3 directories.

The map_config directory contains the CITIC floor plan in SVG (Inkscape file) and PDF: citic_map.svg and citic_map.pdf.
The room_map.json file contains the simplified map with rooms and doors used by our tracker.
The Node*.json files contain the information about every camera: position and calibration parameters.

The ground-truth positions are in the capture*_gt.mot.txt files. The files follow the MOT15 CSV format:

    <frame>, <id>, <bb_left>, <bb_top>, <bb_width>, <bb_height>, <conf>, <x>, <y>, <z>


The BLE information is in the BLE directory:

 - anchor_sensors_citic.json : The BLE beacons positions.
 - beaconreports.json : The complete beacon reports during all the dataset capture process.
 - capture*_beacon_scans.json: The obtained beacon reports for each of the captured sequences.


The ground-truth position files and the beacon report files can be generated by the generate_gt.py script using the following files: paths.csv, timesyncs.csv, and BLE/beaconreports.json.



### License

The CITIC-MTMC dataset is licensed under the [CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/) license. The included source code is provided under the [MIT](CODE_LICENSE) license.

