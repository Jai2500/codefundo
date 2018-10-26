# Code.Fun.Do++
## Drone Processes and Mesh Implementation for data tranfer
A brief documentation on the drone implementation and mesh networking 

### Drone Processes and their pseudo-implementations

 __The drone had the following requirements__
  * GPS Enabled
  * 3-Axis Camera 
  * On-board SoC
  * Connectivity to the Base Stations
 
The drone of our choice is the DJI M200 Series Quadcopters (specifically the M210) with the addition of the Zenmuse Z30 Camera Module due to:
* Their robust design and high enurance to various natural conditions such as high/low temperature and water and dust resistance. 
* Long Battery Life of 38min.
* Inbuilt GPS Support
* Autonomous Flight support (even when it is out of the range of the manual RC).
* Support for the Onboard SDK (the one used), along with the support for Mobile SDK.
* Fairly sufficent Payload capability. 
* The camera module Zenmuse Z30 was specically chosen due to its support for very high zoom capability, which is perfect for high altitude flight as well low altitude flight. 

##### The Basic Working Model of the drone

1. Each drone is connected to either the previous drone or more drones through a mesh network to FANET System. 
2. Each drone is assigned a circular region, the radius of which is given by ![Eq of radius](http://latex.codecogs.com/gif.latex?R%20%3D%20X%20-%202r) ; where *R* is the distance from the previous drone/base (effectively the radius of the drone), *X* is the range of the transmission device, and *r* is the deviation of the drone from the centre of the circular region. 
3. The respective latitude and longitude of the centre of the circular region is then decided, and the first waypoint is set to that.
4. The subsequent waypoints are generated randomly within the circular region such that ![Eq of dev.](http://latex.codecogs.com/gif.latex?x_%7Bi%7D%20-%20x_%7B%5Ccirc%7D%20%3C%20r) ; where ![xi](http://latex.codecogs.com/gif.latex?x_%7Bi%7D) is the radial position of the drone from the centre of the circular region, ![xo](http://latex.codecogs.com/gif.latex?x_%7B%5Ccirc%7D) is the centre of the circular region, and *r* is the max deviation from the centre. 
5. At each waypoint, the drone snaps 4 photos each at ![90](http://latex.codecogs.com/gif.latex?90%5E%7B%5Ccirc%7D) to each other. This is paired with the GPS co-ordinate of the drone and sent to the base station for analysis.
7. The actual distance ![s](http://latex.codecogs.com/gif.latex?s) of the people from the drone is calculated using the equation ![eq dist](http://latex.codecogs.com/gif.latex?tan%20%28%5Calpha%29%20%3D%20%5Cfrac%7Bs%7D%7Bh%7D); where ![alp](http://latex.codecogs.com/gif.latex?%5Calpha) is the angle of depression of the camera of the drone, *s* is the distance of the people from the drone, and *h* is the height of the drone. 
8. After the drone travererses, through all the waypoints it returns back to the base station, and is replaced with another one at the same co-ordinates. An alternate solution is to cascade the drones, so when the first one is out of duty, the second one in line replaces its position so as to still maintain connection to the base station. 

__Code for the latitude and longitude generation__

// Enter the code for Latitude and Longitude Generation.


__Code for the Waypoint Setting and Controlling the Drone__ 

A basic implementation of the algorithm for waypoint was done in __C++__. Due to sheer size and quantity of files, only the *most* important files have been uploaded. The other files are assumed to be understood. 

Link : [C++ Files ](https://1drv.ms/f/s!Am8mfksK8R_6gQY6ujGGNK6M3i8y)

### Mesh Networking (FANET) System

An intuitive solution to the lack of structured communication services in the times of natural disasters is to develop an ad-hoc network among the drones and the rescue operators. This forms what is known as a *Flying Ad-Hoc Network*. 

__Features__
* Each drone is fitted with a Raspberry Pi Model B and a WiFi dongle attached to the Raspberry Pi. 
* A linux based operating system called the __ByzPi__ (developed from Byzantium Operating System) is loaded onto the drones. 
* Any person with a device which has support for AD-HOC Networks can connect. 
* Supports connection to the internet, so as to send information at large distance when required.
* The message sent from one of the drone is relayed across other ones thorugh the most *reliable* path until it reaches the Base Station for processing. 
* Rescue Operator can also send requests to the Base Station using the same Ad-Hoc Network. 
* Upon addition of crendential to each node, it may also be possible to enable crowd sourcing of the information at various locations (and classifying them as weak classifiers, until a suitable number of them results to a considerable amount).
