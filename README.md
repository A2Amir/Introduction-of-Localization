# Introduction of Localization
 Localization answers a question, where is a car or robot in a given map with a high accuracy.

Now assume:

* There is a car that is totally lost, which means you, as a driver or as a car, have no clue where you are. 
* You have a global map of the environment.

  <img src="./img/1.jpg" alt="  a global map of the environment"  style="width: 200px;hight:100px"align="right">

In a traditional way, we use global navigation satellite systems to find the car, with respect to the map. But GPS is not precise enough most of the time and has an accuracy about one to three meters and sometimes it can be as broad as 10 to 50 meters. Clearly this is not reliable enough for a self-driving car. You can't trust GPS and you have to find another technique to localize yourself inside a given map. 

It is common practice to use the onboard sensor data (like RADAR and LIDAR), along with our global map, to solve the localization issue. With the onboard sensors it is possible to measure distances to static obstacles, like trees, poles, or walls.We measure these distances, and the bearing of these static objects in the local coordinate system of our car. 

<p align="right">
  <img src="./img/2.jpg" alt=" a local coordinate system of our cart" style="width: 200px;" >
</P>

Now when you are lucky, the same obstacles that were observed by the on-board sensors are also part of the map. Of course, the map has its own global coordinate system. 

<p align="right">
  <img src="./img/3.jpg" alt=" a global coordinate system" style="width: 300px;" >
</P>
To estimate where the car is in the map, you have to match the observations with the map information and when you do it correctly, this results in a transformation between both coordinate systems (the local car coordinate system and the global coordinate system of the map). This transformation should be as accurate as possible-- let's say within a range of 10 centimetres 


Summarize of localization:

•	Localization answers a question, where is a car in a given map with a high accuracy and high accuracy means between three and 10 centimetres. 

•	A robot gathers information about its current environment and compares that to a known map to understand where it is in the world.


•	On-board sensors are used to estimate the transformation between local measurements and a given map. 

