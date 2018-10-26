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
2. Each drone is assigned a circular region, the radius of which is given by ![Eq of radius](http://latex.codecogs.com/gif.latex?R%20%3D%20X%20-%20r)
