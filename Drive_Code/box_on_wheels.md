## Box on Wheels

You have now opened up a bare bones template to write your robot code; congratulations you’ve made a box on wheels, now to understand what you’re box on wheels does, before you destroy it and create your own completely improved code. It is necessary to understand the classes that created this box on wheels so you know that you just didn’t create another box on wheels program, but it is a good start.

#### ➠ The Code
The drive program in it’s entirety:

```c++
#include “WPILib.h”
//Last modified: January 19, 2014 by: Alan
/*
 This is a demo program showing the use of the RobotBase class.The SampleRobot class is the base of a robot application that will automatically call your
 Autonomous and OperatorControl methods at the right time as controlled by the switches on the driver station or the field controls.
 */
class RobotDemo : public SampleRobot {
    RobotDrive myRobot;	// robot drive system
    Joystick stick;	// only joystick

public:
	RobotDemo(void):
        myRobot(1, 2),	// these must be initialized in the same order
        stick(1)		  // as they are declared above.
	{
		myRobot.SetExpiration(0.1), //you can initialize things here like gyros at construction
	}

// Drive left & right motors for 2 seconds then stop

	void Autonomous(void) {
		myRobot.SetSafetyEnabled(false);
		myRobot.Drive(0.5, 0.5);	// drive forward at half speed
		Wait(2);				    // for 2 seconds
		myRobot.Drive(0.0, 0.0);	// stop robot
	}

// Runs the motors with arcade steering
	void OperatorControl(void) {
		myRobot.SetSafetyEnabled(true);
		while (IsOperatorControl())
		{
			myRobot.ArcadeDrive(stick); // drive with arcade style (use right stick)
		Wait(0.005); // wait for a motor update time
	}
}

// Runs during test mode
    void Test() {

    }
};
START_ROBOT_CLASS(RobotDemo);
```


#### ➠ The Explanation
Breakdown of the code follows as so:

```c++
#include “WPILib.h”
```

This including of the WPI Library is the inclusion of a spellbook for almost every class needed for the robot: motors, pneumatics, Axis cameras, etc.
NOTE: There will still be much time spent using the “WPILib C++ Reference”, but the use of the basic manual reduces most of the time spent by presenting sample/proper usage so the learning process does not need to repeat itself and time can be best allocated elsewhere.

```c++
/*
This is a demo program showing the use of the RobotBase class. The SampleRobot class is the base of a robot application that will automatically call your
Autonomous and OperatorControl methods at the right time as controlled by the switches on the driver station or the field controls.
 */
```

If you’ve commented in programming, then you know what you should be doing, if you are lazy and have some personal belief or dogma that, “Tough beans, figure out my giant program,” you are impeding the progress of your subteam and you are absolutely terrible. However, if you’re just in the mood and have started a program, comment what needs to be understood because you never know when you might be gone the next day and someone else has to run your program.

```c++
class RobotDemo : public SampleRobot

This is your physical robot, RobotDemo is the name of the class, SampleRobot is the class that RobotDemo inherits it’s methods.

{
	RobotDrive myRobot;	// robot drive system
	Joystick stick;	    // only joystick
```

Declaration of the robots parts, `RobotDrive` is a simplified drive system class that declares motors for you and has preprogrammed drive functions; `Joystick` also declared last because it is a part of the robot, but how else are you going to control it? With your mind? I THINK NOT!

```c++
public:
		RobotDemo(void):
        myRobot(1, 2),	// these must be initialized in the same order
        stick(1)		  // as they are declared above.
	{
		myRobot.SetExpiration(0.1), //you can initialize things here like gyros at construction
	}
```

`RobotDemo` is the constructor of your robot, it will now initialize what you declared previously as ports in the sidecar for most of the declared objects, with the exception of the joystick. As noted, `RobotDemo` has the same name as the class because of how objects work, and it is void, but you don’t have to put void as in C++ it automatically assumes void. The pair of braces after you instantiate the ports of your controllers allows you to initialize/run commands (like sensors) at the very beginning.

```c++
// Drive left & right motors for 2 seconds then stop
	void Autonomous(void) {
		myRobot.SetSafetyEnabled(false);
		myRobot.Drive(0.5, 0.5);	// drive forward at half speed
		Wait(2);				// for 2 seconds
		myRobot.Drive(0.0, 0.0);	// stop robot
	}
```

This is the `Autonomous` method of the `RobotDemo` class, and it was inherited from `SampleRobot`. It will only run during the Autonomous period of the game. `SetSafetyEnabled` is to protect everyone in case of loss of communication or other problems when set to true in the `()`. Drive sets the speed of the motors in the order initialized respectively, from a value of (`-1.0` to `1.0`). Wait is a method that stops the program from reading any further lines for the time specified in the `()` in seconds. To stop the robot, the motors after being set to move must be set back to zero.

```c++
// Runs the motors with arcade steering
	void OperatorControl(void) {
		myRobot.SetSafetyEnabled(true);
		while (IsOperatorControl()) {
			myRobot.ArcadeDrive(stick); //drive with arcade style (use right stick)
		    Wait(0.005);	// wait for a motor update time
	    }
    }
```

`OperatorControl` is a method of the `RobotDemo` class, this method was also inherited from `SampleRobot`. This is where the code for your tele-op or driver control period goes. `SetSafetyEnabled` was already mentioned, but as a reminder, it’s for the safety of all others and the robot in case of communication problems with the robot. The while loop is there to make sure that you are always in control during the period, without the loop, the code would only run once and your robot would then become a stationery box. `ArcadeDrive` is the type of drive using arcade joystick, the robot will move according to the joystick input.

```c++
// Runs during test mode
	void Test() {

    }
```

This is where you would input test code that you wouldn’t put into either Autonomous or Tele-op without being sure it would work first or if it would conflict with other parts of the code inside those methods.

```c++
};
START_ROBOT_CLASS(RobotDemo);
```

`START_ROBOT_CLASS` sets up a "user class factory", which is a function that returns a pointer new instance of your robot class. It also creates the entry point function, `FRC_UserProgram_StartupLibraryInit`.