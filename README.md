# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program

### Goals
In this project your goal is to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. You will be provided the car's localization and sensor fusion data, there is also a sparse map list of waypoints around the highway. The car should try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible, note that other cars will try to change lanes too. The car should avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car should be able to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 10 m/s^3.

#### The map of the highway is in data/highway_map.txt
Each waypoint in the list contains  [x,y,s,dx,dy] values. x and y are the waypoint's map coordinate position, the s value is the distance along the road to get to that waypoint in meters, the dx and dy values define the unit normal vector pointing outward of the highway loop.

The highway's waypoints loop around so the frenet s value, distance along the road, goes from 0 to 6945.554.

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./path_planning`.

## Rubric points

### Compilation
Code compiled with cmake and make. 
A new file was added src/spline.h. It is the Cubic Spline interpolation implementation: a single .h file you can use splines instead of polynomials.

### Valid Trajectories
#### The car is able to drive at least 4.32 miles without incident
-- working fine (unable to check in my system due to low system configuration

#### The car drives according to the speed limit.
No speed limit red message was seen.

#### Max Acceleration and Jerk are not Exceeded.
Max jerk red message was not seen.

#### Car does not have collisions.
No collisions.

#### The car stays in its lane, except for the time between changing lanes.
The car stays in its lane most of the time but when it changes lane because of traffic or to return to the center lane.

#### The car is able to change lanes
The car change lanes when the there is a slow car in front of it, and it is safe to change lanes (no other cars around) or when it is safe to return the center lane.)

### Reflection
Based on the provided code from the seed project, the path planning algorithms start at src/main.cpp line 246 to the line 416. 

The code consist of three parts:

#### Prediction 
This part of the code deal with the telemetry and sensor fusion data. It intents to reason about the environment. In the case, we want to know three aspects of it:

Is there a car in front of us blocking the traffic.
Is there a car to the right of us making a lane change not safe.
Is there a car to the left of us making a lane change not safe.
These questions are answered by calculating the lane each other car is and the position it will be at the end of the last plan trajectory. A car is considered "dangerous" when its distance to our car is less than 30 meters in front or behind us.

#### Behavior 
This part decides what to do:

If we have a car in front of us, do we change lanes?
Do we speed up or slow down?
Based on the prediction of the situation we are in, this code increases the speed, decrease speed, or make a lane change when it is safe. Instead of increasing the speed at this part of the code, a speed_diff is created to be used for speed changes when generating the trajectory in the last part of the code. This approach makes the car more responsive acting faster to changing situations like a car in front of it trying to apply breaks to cause a collision.

#### Trajectory 
This code does the calculation of the trajectory based on the speed and lane output from the behavior, car coordinates and past path points.

## Reference
Few ideas for the project implementation taken from https://github.com/darienmt/CarND-Path-Planning-Project-P1




