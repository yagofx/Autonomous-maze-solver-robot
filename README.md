# Autonomous-maze-solver-robot
Maze solver robot with Arduino

The first serious project that I developed with my classmates in my first year of High Schoool was to create a robot that could solve autonomously a maze. I was able to acquire an Arduino robot with two wheels that could rotate. We decided to use three ultrasound sensors to be to detect the distance of the walls on the left, front and right. Through those inputs, we were able to detect which one of the cases the robot was at every moment.

The first part of the code was the definition of all the inputs, variables and parameter that we were going to be using.

We can see first how we define the pin inputs of the 3 ultrasound sensors, one for the echo with 3 pins and another for the trig with 3 more, one for every single sensor.
Afterwards, we define the float variable to calculate the distances such as the t[] and d[] and so on. Also, we define the variables to store the environment such as the front wall f_w, l_w and r_w. If this integer was 1 it was a wall if it was a 0 it wasn't. We also defined the pins of the motors and the power of them. And finally, we defined some boolean variables that we needed. There's also the time to move forward one block and to rotate 90 degrees.

This second part of the code defines three functions. These are the ones that when they are called on the main function that runs on a loop on the Arduino are going to calculate the distance of the front, left and right. Inside every function we can see that we send a signal through the trig, that's we make sure first it is low and then we send a pulse. Then we calculate the time using the "pulse" function that returns the time when the "echo_p" gets high. Then I make sure that the distance is constrained with the "constrain" function that limits this variable between 1 to 30. That is because the ultrasound sensor doesn't work against objects very close and too far.

The following code is just the functions that turn on the wheel to move forward, left and right. However, when we were testing the code we encountered one problem. As expected the robot cannot turn with accuracy 90 degrees to the left and the right, therefore when it moves forward it crashes against a wall. That's why we came up with the idea to not just move forward, it self-corrects to the middle of the maze. We perfected this method through testing and it worked pretty well.

On this part of the code, we also defined a function called stop_all that makes sure that every motor is stopped even though on the previous functions we also called them off

The function setup is run once every time the Arduino is initialized. In our case, we define the following variables as inputs or outputs.

The next part of the code is the main code of the program and the most important one. This one called "loop" runs constantly the code inside him.

First, we check if the variable move is false, in this case, we call the l three functions that calculate the distance of the three sensors. Once the distance is calculated we wanna define if there is a wall or not, that's why if on the front there's less than 25 cm we set the f_w to 1, that's how we define that on the front wall, there's a wall. And the same on the left and right but the threshold is 20 cm. Then we run those variables through consecutive if to know what of the 7 cases we are.

If It is case 0, that means we are only able to move forward and we run the forward function, we also set other variables that I will explain later.

If it is case 1 then we check if the fake and rot booleans are false and then we move forward, rotate 90 degrees to the right and we move forward another time.

If It is case 2, we check if the fake and rotate are both false, if it is the case we move forward if it is not then we rotate 90 degrees straightaway without moving forward and then we move forward.

If It is case 3, we check if the fake and rotate are both false, if it's the case we move forward if it isn't we check the prior variable. If It is false that means that the priority of the robot will be to go to the left or else it will rotate to the right and move forward.

If It is case 4, if the check is false then we move forward if It isn't we won't. Then we'll check if the prior is false if it is then we'll move forward straight away if it isn't we'll turn to the right and then we'll move forward.
If It is case 5, if fake is false then will move forward, if prior is false we'll turn left and move forward or else we'll just move forward.

If it is case 6, it means that we are on a dead-end so we'll turn 180 degrees. We added an extra if to confirm it was a dead-end because sometimes the robot detected a dead-end where it wasn't because it wasn't always parallel to the walls.

And the last piece of code prints the variables to the serial monitor so that when we were testing we could know what was going on.

It might be mistake the code and It isn't very optimized but we gave our best to this project and it finally made it out of the maze. I wish I had photographs and videos of this project but I couldn't find any.
