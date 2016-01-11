# Microswitch

### ➠ Use
![](microswitch.jpg)

The microswitch is usually used to keep something from overextending or surpassing some distance. When the switch not pushed, the switch is NC (normally closed), returning 1. When the switch pushed, the switch is  NO (Normally Open), returning 0.


### ➠ Wiring 
![](microswitchwiringdiagram.png)
![](microswitchwiring.png)

The switch is plugged into the Digital IO section of the roboRIO via a PWM cable.

### ➠ Programming
Declared and instantiated as a `DigitalInput`
* When switch NC, returns 0
* When switch NO, returns 1

Declaration: `DigitalInput switch;`

Instantiation: `switch (1) //port number in the digital sidecar`

Using Microswitch: `switch.Get(); //returns either 0 or 1`

**// A Barebones Code**
```c++
#include "WPILib.h"
// Last modified: February 7, 2014 by: Vivian
class RobotDemo : public SampleRobot {
	DigitalInput limitSwitch;
public:
	RobotDemo(void):
		limitSwitch(1) {
		
	}

	void Autonomous(void) {

	}
	
	void OperatorControl(void) {
		while (IsOperatorControl())
		{
			if(limitSwitch.Get() == 1) {
                // you can do things here if the switch is pressed
            }
		}
	}
	void Test() {
		while(IsTest()) {
		
		}
	}
};
START_ROBOT_CLASS(RobotDemo);
```