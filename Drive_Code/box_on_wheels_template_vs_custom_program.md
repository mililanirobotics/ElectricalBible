## Box on Wheels Template vs Custom Program

While Box on Wheels Template is already made, there is not a lot of room to edit this drive code unless you are using two Logitech Extreme 3D Pro USB Joysticks.
If you search in the WPILib Reference for RobotDrive, the constructors and drive methods are designed for something like the above. Also your choices of # of motors for drive is only either 2 or 4. If you wish to use a Logitech F310 Gamepad, you are better off writing your own drive code.
When I mean custom, delete the unnecessary parts of the template that would be not conducive to the word custom. Below is barebones code that you may modify to meet your own desires.

#### ➠ The Code

```c++
#include "WPILib.h”
//Last modified: January 25, 2014 by: Alan
class RobotDemo : public SampleRobot {
	Joystick stick;

public:
	RobotDemo(void):
	stick(1) {
	}
	// Insert your own comment
	void Autonomous(void)
	{
	}

	// Insert your own comment
	void OperatorControl(void) {
		while (IsOperatorControl()) {
			Wait(0.005);	// wait for a motor update time
		}
	}
	// Insert your own comment
	void Test() {
	}
};
START_ROBOT_CLASS(RobotDemo);
```

#### ➠ The Explanation
Here’s a pancake sandwich with sprinkles.

```c++
#include "WPILib.h"
```

This is your spellbook. Live it, breathe it.

```c++
class RobotDemo : public SampleRobot
```

The `RobotDemo` class + `SampleRobot` from the template gives you the inherited methods to use in the Driver Station, will need it

```c++
Joystick stick;
```

You will always need a joystick, again, unless you can control your robot with your mind, or it is completely autonomous, make the joystick.

```c++
public:
	RobotDemo(void):
		stick(1)
	{
	}
```

Instantiate the stick, you can’t use it if you don’t instantiate it. The braces have to be there, part of the compiling. When you start adding in motors and sensors, their expirations/initialization will be set in those braces.

```c++
	void Autonomous(void) {
	}
```

Still need autonomous section, part of the inheritance. If you use it or not is up to that year’s game, but you still need this!

```c++
	void OperatorControl(void) {
		while (IsOperatorControl()) {
		    Wait(0.005);	// wait for a motor update time
		}
	}
```

This is where you write the god code, where you let your driver feel like a king moving the robot...with your code :D Make sure the code that will let the driver execute commands is in the while loop, wouldn’t it suck that they can only do it once because it was not in the loop? Before the loop is when you can instantiate specific things such as the resolution of an axis camera.

```c++
	void Test() {
	}
```

Testing space for small portions of questionable code. Also part of inheritance, required.

```c++
};
START_ROBOT_CLASS(RobotDemo);
```

Closes brace from the beginning of the class. `START_ROBOT_CLASS(RobotDemo);` notice how `RobotDemo` is in the parameter, isn’t that the class? So this is also important for it runs the class.
