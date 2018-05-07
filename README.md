# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

## [Rubric](https://review.udacity.com/#!/rubrics/824/view) points


### Your code should compile.

The code compiles without errors or warnings. No modifications were done on the provided setup.

### The PID procedure follows what was taught in the lessons.

The PID implementation is done on the [./src/PID.cpp](./src/PID.cpp). The [PID::UpdateError](./src/PID.cpp#L25) method calculates proportional, integral and derivative errors and the [PID::TotalError](./src/PID.cpp#L39) calculates the total error using the appropriate coefficients.

### Describe the effect each of the P, I, D components had in your implementation.

- The proportional component of the controller tries to steer the car toward the center line (against the cross-track error). If used along, the car overshoots the central line very easily and go out of the road very quickly. An example video where this component is used along is [./videos/P_Only.mp4](./videos/P_Only.mp4).

- The integral component tries to eliminate a possible bias on the controlled system that could prevent the error to be eliminated. If used along, it makes the car to go in circles. In the case of the simulator, no bias is present.

- The differential component helps to counteract the proportional trend to overshoot the center line by smoothing the approach to it. An example video where this component is used is [./videos/PID_Final.mp4](./videos/PID_Final.mp4).

### Describe how the final hyperparameters were chosen.

The parameters were chosen manually by try and error.
First, I've set the parameters to zeros to make sure that the car can drive in straight line. As i found that it can keep the straight line that means that the simulator does not enforce any bias on the vehicle.
Then add the proportional, I started with the value "1" and the car start stearing in the road but it the was a big overshooting. I tried to inclease the value to 2 and i found that the overshooting increases so i decided to go to 0.5 which showed a good result with small overshooting. Again I tried to decrease the value to 0.2 and I found that the result is so how better, here is decided to freez the "P" parameter at "0.2"
Then add the differential to try to overcome the overshooting. I started with 1 which caused to car to successfully follow the trace but there were some overshooting at the sharp turns, I incleased the value to 2 which minimized the overshooting but caused CTE to increase at the sharp turns. Finally i decided to select 1.8 as it gave me a good balance between overshooting reduction and CTE value.

The final parameters where [P: 0.2, I: 0.0, D: 1.8].

### The vehicle must successfully drive a lap around the track.

A short video with the final parameters is [./videos/PID_Final.mp4](./videos/PID_Final.mp4).

