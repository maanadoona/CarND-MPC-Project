# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

[image0]: ./images/DynamicModel.png
[image1]: ./images/GlobalKinematicModel.png
[image2]: ./images/ModelPredictiveControl.png
[image3]: ./images/CrossTrackError.png
[image4]: ./images/OrientationError.png

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

[location X, location Y, angle, velocity, CrossTrackError, Orientation Error]

![alt text][image1]

![alt text][image3]

![alt text][image4]


### 2. Timestep Length and Elapsed Duration (N & dt)
N : the number of timesteps in the horizon
dt : how much time elapses between actuations
==> T = N*dt

Larger dt results in less frequent actuation. It makes harder to accurately approximate a continuous reference trajectory.
So, smaller dt is better than larger.
If N is larger then T (time to measure) is larger. It makes time longer to compute.

I tried to set various values between N and dt. Finally, I got the N=10, dt=0.1 is proper in experimentally.



### 3. Polynomial Fitting and MPC Preprocessing
To make polynomial fitting and MPC preprocessing, We should follow the next steps.
1. Set N and dt.
2. Fit the polynomial to the waypoints.
3. Calculate initial cross track error and orientation error values.
4. Define the components of the cost function (state, actuators, etc). You may use the methods previously discussed or make up something, up to you!
5. Define the model constraints. These are the state update equations defined in the Vehicle Models module.

1. Polynomial fitting e.g. to 3rd order, and
2. Waypoints pre-processing e.g. coordinate transform
Third degree polynomials are common so they can fit most roads. From road's path, we should calculate the car's position and direction. So, it need to transform the coordinates. 

### 4. Model Predictive Control with Latency
I set the latency as 100milliscond.

![alt text][image2]



## Simulation
Finally, I have driven the car in course safely. 

I analyzed and tuned the cost function and it's parameters.

A - Part of the reference state
B - Part of the use of actuators
C - Part of the value gap between sequential actuations

I found that A, B is major and C is minor on effects.
A is related to follow the reference line.
B is related to spin and to recover their direction.
C helps their recovering but effect is small.

I got the own parameters to finish the drive in course. But I think it's not the best for optimization.
Thank you.
