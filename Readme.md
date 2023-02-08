# CITIC-MTMC dataset

This repository contains the CITIC-MTMC dataset.

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

This script uses the obtained information from the Checkpoint Manager application:

 - [Backend](https://github.com/GTEC-UDC/checkpoint-manager-backend)
 - [Admin](https://github.com/GTEC-UDC/checkpoint-manager-admin)
 - [Mobile application](https://github.com/GTEC-UDC/CheckpointManagerNative) for iOS and android.


### License

The CITIC-MTMC dataset is licensed under the [CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/) license. The included source code is provided under the [MIT](CODE_LICENSE) license.

