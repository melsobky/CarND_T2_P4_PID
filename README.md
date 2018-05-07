# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

## [Rubric points](https://review.udacity.com/#!/rubrics/824/view)


### Your code should compile.

The code compiles without errors or warnings. No modifications were done on the provided setup.

### The PID procedure follows what was taught in the lessons.

* The PID implementation is done in the [./src/PID.cpp](./src/PID.cpp). 
* The [PID::UpdateError](./src/PID.cpp#L25) method calculates proportional, integral and derivative errors
* The [PID::TotalError](./src/PID.cpp#L39) calculates the total error using the appropriate coefficients.

### Describe the effect each of the P, I, D components had in your implementation.

- The proportional component of the controller tries to steer the car toward the center line (against the cross-track error). If used alone, the car overshoots and go out of the road very quickly. An example video where this component is used along is [./videos/P_Only.mp4](./videos/P_Only.mp4).

- The integral component tries to eliminate a possible bias on the controlled system that could prevent the error to be eliminated. If used along, it makes the car to go in circles. In the case of the simulator, no bias is present.

- The differential component helps to counteract the proportional trend to overshoot the center line by smoothing the approach to it. An example video where this component is used is [./videos/PID_Final.mp4](./videos/PID_Final.mp4).

### Describe how the final hyperparameters were chosen.

- The parameters were chosen manually by try and error.
- First, I've set the parameters to zeros to make sure that the car can drive in straight line.
- As i found that it can keep the straight line that means that the simulator does not enforce any bias on the vehicle.
- Then add the proportional, I started with the value "1" and the car start stearing in the road but it the was a big overshooting.
- I tried to inclease the value to 2 and i found that the overshooting increases so i decided to go to 0.5 which showed a good result with small overshooting.
- Again I tried to decrease the value to 0.2 and I found that the result is so how better, here is decided to freez the "P" parameter at "0.2"
- Then I added the differential to try to overcome the overshooting.
- I started with 1 which caused to car to successfully follow the track but there were some overshooting at the sharp turns.
- I incleased the value to 2 which minimized the overshooting but caused CTE to increase at the sharp turns.
- Finally i decided to select 1.8 as it gave me a good balance between overshooting reduction and CTE value.

The final parameters where [P: 0.2, I: 0.0, D: 1.8].

### The vehicle must successfully drive a lap around the track.

A short video with the final parameters is [./videos/PID_Final.mp4](./videos/PID_Final.mp4).
