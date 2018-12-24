# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

[image0]: ./images/DynamicModel.png
[image1]: ./images/GlobalKinematicModel.png
[image2]: ./images/ModelPredictiveControl.png

## Project Goal
In this project you'll implement Model Predictive Control to drive the car around the track. This time however you're not given the cross track error, you'll have to calculate that yourself! Additionally, there's a 100 millisecond latency between actuations commands on top of the connection latency.

## Compilation
1. Clone this repo.
2. Make a build directory: mkdir build && cd build
3. Compile: cmake .. && make
4. Run it: ./mpc.


## Implementation
### 1. The Model
 I designed the model to follow the reference path on the road like below
![alt text][image0]

I implemented the code like below.

![alt text][image1]


### 2. Timestep Length and Elapsed Duration (N & dt)
N : the number of timesteps in the horizon
dt : how much time elapses between actuations
==> T = N*dt


### 3. Polynomial Fitting and MPC Preprocessing
To make polynomial fitting and MPC preprocessing, We should follow the next steps.
1. Set N and dt.
2. Fit the polynomial to the waypoints.
3. Calculate initial cross track error and orientation error values.
4. Define the components of the cost function (state, actuators, etc). You may use the methods previously discussed or make up something, up to you!
5. Define the model constraints. These are the state update equations defined in the Vehicle Models module.


### 4. Model Predictive Control with Latency
I set the latency as 100milliscond.

![alt text][image2]



## Simulation
Finally, I have driven the car in course safely. 



