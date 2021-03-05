# CARLA_Motion_Planning_for_Self-Driving_Cars_Project
This project implements a functional motion planning stack for autonomous vehicles to avoid both static and dynamic obstacles while 
tracking the center line of a lane, while also handling stop signs. The path generated by the motion planner is executed by the 
vehicle controller, which was designed in my another project [here](https://github.com/yymmaa0000/CARLA_Self-Driving_Vehicle_Control_Project).

This project is a part of the Self-Driving Cars Specialization course in Coursera. The detail about this specialization can be found [here](https://www.coursera.org/specializations/self-driving-cars).

The performance of the motion planner was simulated using the CARLA simulator, which is a modified version of the original CARLA simulator 
with additional maps included. If you wish to try my controller yourself, please download and install this simulator following the 
instructions [here](https://www.coursera.org/learn/motion-planning-self-driving-cars/supplement/i9R3x/carla-installation-guide). To learn 
how to use this simulator, you can refer to the project instruction from Coursera 
website [here](https://www.coursera.org/learn/motion-planning-self-driving-cars/programming/wiGwg/course-4-final-project).

To design a reliable motion planner, I implemented behavioral planning logic, as well as static collision checking, path selection, and velocity profile generation.
The files named "behavioural_planner.py", "collision_checker.py", "local_planner.py", "path_optimizer.py", and "velocity_planner.py" contains
these 5 main aspects of the planner.

The screen recording of the simulation for an autonomous driving scenario in a small town can be viewed in YouTube: https://youtu.be/uX1YVPuVU0Q

### Trajectory of the car driving through a small town road: ###

![alt text](https://github.com/yymmaa0000/CARLA_Motion_Planning_for_Self-Driving_Cars_Project/blob/master/controller_output/trajectory.png)

### Implementation detail: ###
Behaviour Planning Logic: use state machine that transitions between lane following, deceleration to the stop sign, staying stopped, and back to lane following, when it encounters a stop sign.

Path Generation: use path optimization to compute a cubit spiral for each given goal point to ensure a confortable and efficient path. The goal points are sampled by laterally offsetting from the goal location along the direction perpendicular to the goal yaw of the ego vehicle.

Static Collision Checking: circle-based collision checking.

Path Selection: eliminate paths that are in collision with static obstacles, and select path according to how closely it follows the lane centerline, and how far away it is from other paths that are in collision.

Velocity Profile Generation: generate a linear ramp and trapezoidal velocity profiles that can handle stop signs, lead dynamic obstacles, as well as nominal lane maintenance, while integrating comfort constaints .