Self-Driving car nanodegree Term3
# Path Planner Project
                      written by Koichi Takabatake

## Summery
My path planner calculate the cost of each behavior first, and after that generate the path by using the calculated velocity and lane.

Below I will show you details of each of them.

### 1. cost function
To decide what to behave, calculate the cost of each behave.
First, correct the sensor fusion data to know whether if there is the car near the front or back of my car.
And give the corrected data to cost function to calculate the cost of each behavior.
Keep lane in max speed or slow down or change lane to left, or right.
I didn't use finite state machine. I used only "lane changed flag" instead.
When lane is changed, then flag is set to true.
When lane isn't changed, then flag is set to false.
And also I didn't predict the other car's behavior.
This is sufficient for this simple traffic.
The code is written in line 411 to 594 in main.cpp.

### 2. generate trajectory
When the decision is made, set velocity and lane.
And they are used to generate trajectory.
Trajectory is consist of previous car coordinates and next coordinates.
First previous path is feed to next path vector.
And then I calculate next path points.
To calculate next path coordinate, I use the last two points of previous path and equally separated destination points. The lane of destination points is set by the one decided by cost function.
And by feeding the next coordinates to spline, trajectory curve is generated.
This trajectory leads to the horizon, in this case, 30 of x.
And trajectory is devided by equally range. The range is the distance which the car run in 0.02 second. The velocity decided by the cost is used here.
And the points are given to next path vector.
So the path is smoothly curves.
In this case, I didin't calculate jerk minimizing trajectory. I only adjusted the parameter for jerk minimizing.
The code is written in line 657 to 749 in main.cpp.

And there it is! The path planner generate the path to drive safely.
