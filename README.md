## Sending body pose data to Microbit

### Description

The framework uses a machine learning model (Tensorflow's BlazePose) to detect one or more 'bodies' from the browser's camera and sends positional data to the Microbit for each body's parts (e.g. 'left wrist', 'right wrist', 'nose', etc.) depending on what has been selected. On the Microbit the data can be used control e.g. light, sound, motion, etc. A simple and relatively trivial example would be to turn the sound volume when wrists are moving away from each other and down when they move closer. 

### Setup
To use the framework you first need to connect the Microbit to your computer and download the code that enables receiving body data from the computer's camera. The code is found here: https://makecode.microbit.org/_WHdhjAYtqRbr

On the Makecode web page, first press 'Edit Code', then press the three dots '...' right of 'Download' button to connect your device. When the device is connected press 'Download' to get the code onto the Microbit. 

After the Microbit is setup you should run the index.html in this folder on a webserver and access it from a browser with a camera. When page is loaded (might take a few seconds) it will access the camera and begin detecting any bodies in the camera feed. Press the 'Connect' button and positional data on selected body parts will be send to the Microbit. 

Pressing 'Disconnect' will often fail. In that case you should reload the page.

### Usage
The code running on the Microbit is written in Typescript. In Makecode you can choose to program visually or writing Typescript code directly. The part of the code relevant for your purposes are the following helper functions: getX, getY, getZ, getSpeed, getConfidence. 

Each of the functions take a 'bodyPartId' as parameter, which is the name of the body part you want data on. If you, for example, want to access the speed of the nose you would write: getSpeed('nose') and it will return the current speed of the nose in m/s (updated every 250ms). If you want the 'y' position of the left eye would write: getY('left_eye') and so on. The getConfidence returns a number between 0-1 which indicates how confident the machine learning algorithm is bodyPart data. The more of the body that is visible on the camera, the better the algorithm works. Be aware that you need to select the body parts you work with on the web page running in the browser, otherwise no data will be received. The full list of bodyPartId's are: 

"nose",
"left_eye",
"right_eye",
"left_ear",
"right_ear",
"left_shoulder",
"right_shoulder",
"left_elbow",
"right_elbow",
"left_wrist",
"right_wrist",
"left_hip",
"right_hip",
"left_knee",
"right_knee",
"left_ankle",
"right_ankle"

The positional data are in meters and goes from -1 to 1 in all three dimensions. The body's hip is center and will have x=0, y=0, z=0. That means that the body is placed inside a cubic space of 2x2x2m:

Extreme bottom: 1m
Extreme top: -1m

Extreme left: 1m
Extreme right: -1m

Extreme back: 1m
Extreme front: 1m

![cubic space of 2x2x2m](/images/blazepose.gif)
### Resources
For a brief introduction to the BlazePose framework see: 
https://blog.tensorflow.org/2021/08/3d-pose-detection-with-mediapipe-blazepose-ghum-tfjs.html 