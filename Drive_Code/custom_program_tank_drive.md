## Custom Program (Tank Drive)
An example of where the driver uses the Logitech F310 Gamepad, but because of the way the RobotDrive class is made, it is preferable to make one’s own code.

####➠ The Code
```c++
#include "WPILib.h"	// WPILibrary.h
#include "Math.h"	// Math.h required for fabs function
//Last modified: January 30, 2014 by: Alan
class RobotDemo : public SampleRobot {
	Talon frontLeft, frontRight, backLeft, backRight; //Talon Motor Controllers
	Joystick logitech; 	// Logitech F310 Gamepad/Controller

public:
	RobotDemo(void):
		frontLeft(1),
		frontRight(2),
		backLeft(3),
		backRight(4),
		logitech(1)
/*
 * Set motor expiration to prevent unwarranted movement if connection lost or
 * disabled
 */
	{
		frontLeft.SetExpiration(0.1),
		frontRight.SetExpiration(0.1),
		backLeft.SetExpiration(0.1),
		backRight.SetExpiration(0.1);
	}

	void Autonomous(void) {
	}

	/**
	 * Runs the motors with tank steering
	 */
	void OperatorControl(void) {
		while (IsOperatorControl()) {
			if(fabs(logitech.GetRawAxis(2)) > 0.2) {
			    /*left joystick, forward & back*/	
			    frontLeft.Set(logitech.GetRawAxis(2) * -.65);
				backLeft.Set(logitech.GetRawAxis(2) * -.65);
			}
			else {
				frontLeft.Set(0);
				backLeft.Set(0);
			}
			if(fabs(logitech.GetRawAxis(4)) > 0.2) {
			    /*right joystick, forward & back*/ 
			    frontRight.Set(logitech.GetRawAxis(4) * .65);
				backRight.Set(logitech.GetRawAxis(4) * .65);
			}
			else {
				frontRight.Set(0);
				backRight.Set(0);
			}
				Wait(0.005);	// wait 0.005 seconds before repeating loop
		}
	}

	/**
	 * Runs during test mode
	 */
	void Test() {
		while(IsTest()) {
		}
	}
};
START_ROBOT_CLASS(RobotDemo);
```

#### ➠ The Explanation

```c++
#include "WPILib.h"	// WPILibrary.h
#include "Math.h"	// Math.h required for fabs function
```

`WPILib.h` is always our spellbook. `Math.h` is a different library that is generally used in C++ for math functions. As stated in the comment, it is used for the `fabs` (float absolute value) function that appears in the tank drive portion of this code.

```c++
class RobotDemo : public SampleRobot
{
	Talon frontLeft, frontRight, backLeft, backRight; //Talon Motor Controllers
	Joystick logitech; 	// Logitech F310 Gamepad/Controller
```

`RobotDemo` class with inherited methods from `SampleRobot` makes templating easier. The talons are one of several motor controllers explained in an earlier section of this manual. `RobotDrive` in the original template declares them in the background, but then you are limited to it’s drive methods. This custom program uses a logitech gamepad which is one joystick object. If you look in the WPILib reference, it will show that to use the tank drive method of the `RobotDrive`, you need two joysticks.

```c++
public:
	RobotDemo(void):
		frontLeft(1),
		frontRight(2),
		backLeft(3),
		backRight(4),
		logitech(1)
// Set motor expiration to prevent unwarranted movement if connection lost or disabled
	{
		frontLeft.SetExpiration(0.1),
		frontRight.SetExpiration(0.1),
		backLeft.SetExpiration(0.1),
		backRight.SetExpiration(0.1);
	}
```

Now in the constructor, the motor controllers are instantiated in the ports of the digital sidecar corresponding to the number in the parentheses. The joystick is instantiated using the USB port. As mentioned in the comment, inside the other braces, there are `SetExpiration`s to prevent continued movement in event of disablement or lost connection. It does this by shutting down power to the object that has expired; now as long as you’re connected, the motors are “fed” and the expirations refresh.

```c++
	/**
	 * Insert own comment
	 */
	void Autonomous(void) {
	}
```

Autonomous code goes here. However this custom program is to show tank drive not full autopilot.

```c++
	/**
	 * Runs the motors with tank steering
	 */
	void OperatorControl(void) {
		while (IsOperatorControl()) {
			if(fabs(logitech.GetRawAxis(2)) > 0.2) {
			    /*left joystick, forward & back*/	
			    frontLeft.Set(logitech.GetRawAxis(2) * -.65);
				backLeft.Set(logitech.GetRawAxis(2) * -.65);
			}
			else {
				frontLeft.Set(0);
				backLeft.Set(0);
			}
			if(fabs(logitech.GetRawAxis(4)) > 0.2) {
			    /*right joystick, forward & back*/ 	
			    frontRight.Set(logitech.GetRawAxis(4) * .65);
				backRight.Set(logitech.GetRawAxis(4) * .65);
			}
			else {
				frontRight.Set(0);
				backRight.Set(0);
			}
			Wait(0.005);	// wait for a motor update time
		}
	}
```

This here is the juicy part, this is tank drive. For those who do not know tank drive, one joystick controls one side of the drive, so when one stick is pushed, only one side moves and the other joystick controls the other respective side. This is where the fabs function is used to shorten coding lines. Normally there would have to be two conditions in those ifs for tank drive to work; if the joystick is greater than a threshold OR if the joystick is below negative threshold. It would look like `joystick.GetRawAxis(2) > 0.2 || joystick.GetRawAxis(2) < -0.2`. Compared to what is in there, it is much easier to code, but less understandable. Reasoning is when you tilt the joystick back it is negative, but it does not pass > `0.2`. Use `fabs` or absolute value(for floats, just abs for ints), less coding.

```c++
	/**
	 * Runs during test mode
	 */
	void Test() {
		while(IsTest()) {
		}
	}
};
START_ROBOT_CLASS(RobotDemo);
```

Closes brace from the beginning of the class. `START_ROBOT_CLASS(RobotDemo);` notice how `RobotDemo` is in the parameter, isn’t that the class? So this is also important for it runs the class.


