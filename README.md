# Introduction of Localization
 Localization answers a question, where is a car or robot in a given map with a high accuracy.

Now assume:

* There is a car that is totally lost, which means you, as a driver or as a car, have no clue where you are. 
* You have a global map of the environment.


<p align="right"> <img src="./img/1.jpg" style="right;" alt="" width="600" height="400"> </p> 

In a traditional way, we use global navigation satellite systems to find the car, with respect to the map. But GPS is not precise enough most of the time and has an accuracy about one to three meters and sometimes it can be as broad as 10 to 50 meters. Clearly this is not reliable enough for a self-driving car. You can't trust GPS and you have to find another technique to localize yourself inside a given map. 

It is common practice to use the onboard sensor data (like RADAR and LIDAR), along with our global map, to solve the localization issue. With the onboard sensors it is possible to measure distances to static obstacles, like trees, poles, or walls.We measure these distances, and the bearing of these static objects in the local coordinate system of our car. 

<p align="right"> <img src="./img/2.jpg" style="right;" alt=" a local coordinate system of our car" width="600" height="400"> </p> 

Now when you are lucky, the same obstacles that were observed by the on-board sensors are also part of the map. Of course, the map has its own global coordinate system. 

<p align="right"> <img src="./img/3.jpg" style="right;" alt=" a global coordinate system" width="600" height="400"> </p> 

To estimate where the car is in the map, you have to match the observations with the map information and when you do it correctly, this results in a transformation between both coordinate systems (the local car coordinate system and the global coordinate system of the map). This transformation should be as accurate as possible-- let's say within a range of 10 centimetres 


Summarize of localization:

* Localization answers a question, where is a car in a given map with a high accuracy and high accuracy means between three and 10 centimetres. 

* A robot gathers information about its current environment and compares that to a known map to understand where it is in the world.


* On-board sensors are used to estimate the transformation between local measurements and a given map. 

## Localization

The question is, how can a car know where it is with an accuracy of 10 cm? That is the localization question, which plays a key role. Localization has a lot of math, but before diving into mathematical detail, I want to give you an intuition for the basic principles. 

#### * Uniform Distribution: prior
You can think of a world with 5 different cells or places where each cell has the same probability that the robot might be in that cell. So probabilities add up to 1. 


<p align="right"> <img src="./img/4.jpg" style="right;" alt=" prior" width="600" height="400"> </p> 

As known the probability that the robot might be in a cell is 0.2 for each cell and the total probability is 1. We can code it like below in python:

```python
p=[]
n=5

for i in range(n):
    p.append(1./n)

print p
```
#### * Probability after Sense:
Let's look at the measurement of this robot in its world with 5 different grid cells (x1-x5). Assume 2 of those cells are colored red whereas the other three are green. As before, we assign uniform probability to each cell of 0.2 and our robot is now allowed to sense. What it sees is a red color. 

<p align="right"> <img src="./img/5.jpg" style="right;" alt=" •	Probability after Sense" width="600" height="400"> </p> 

**How will this affect my belief over different places?**

Obviously, the one's for x2 and x3 should go up and the ones for x1, x4, and x5 should go down. To tell you how to incorporate this measurement into our belief with a very simple rule(a product). Any cell where the color is correct (red cell) we multiply it with a relatively large number (say, 0.6) whereas all the green cells will be multiplied with 0.2.

If we look at the ratio of those, then it seems about 3 times as likely to be in a red cell than it is to be in a green cell, because 0.6 is 3 times larger than 0.2. After multiplying, result would be like below:


<p align="right"> <img src="./img/6.jpg" style="right;" alt=" affected  belief over different places" width="600" height="400"> </p> 


You may notice that the probabilities do not add up to one(the probability distribution always have add up to one), which should be fixed by learning about renormalization.


