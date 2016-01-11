# roboRIO Accelerometer
### ➠ General Overview
![](roborio_acc.png)
One of the many features that comes with the RoboRIO is the built-in 3-axis accelerometer, which has the potential to replace the ADXL345 accelerometer that also comes in the 2015 Kit of Parts. The purpose of this device is to determine the proper acceleration of an object, which is its acceleration relative to freefall. This can be used to determine how much the robot is tilted or a way to monitor motion.

### ➠ Specifications
* Axes: 3 (x, y, and z)
* Sample Rate: 800 Samples per second
* Resolution: 12 bits
* Range: ±8g (gravity)
* Noise: 3.9 mgms typical at 25° C


###➠ The Code
This is the code we used to determine the direction of each axis as well as the stability of the returned values.

```c++
#include "WPILib.h"

class Robot: public SampleRobot
{
	BuiltInAccelerometer accelerometer;

	const double kUpdatePeriod = 0.005; // 5milliseconds / 0.005 seconds.
public:
	//sets the range of the accelerometer to be + or - 8G (units of gravity)
	Robot() : accelerometer(Accelerometer::Range::kRange_8G)
	{
	}
	void OperatorControl()
	{
		double xAcceleration;	//acceleration on the x-axis
		double yAcceleration;	//acceleration on the y-axis	
		double zAcceleration;	//acceleration on the z-axis
		double previousX = 0;	//Previous recursive average on x-axis
		double previousY = 0;	//Previous recursive average on y-axis
		double previousZ = 1;	//Previous recursive average on z-axis

		while (IsOperatorControl() && IsEnabled())
		{
			xAcceleration = accelerometer.GetX(); //returns x-axis accel
			yAcceleration = accelerometer.GetY(); //returns y-axis accel
			zAcceleration = accelerometer.GetZ(); //returns z-axis accel

			SmartDashboard::PutNumber("X-Axis G:", xAcceleration);
			SmartDashboard::PutNumber("Y-Axis G:", yAcceleration);
			SmartDashboard::PutNumber("Z-Axis G:", zAcceleration);

			SmartDashboard::PutNumber("Recrusive X-Axis Average:", ((xAcceleration*0.1) + (0.9*previousX)));
			//returns a recursive average for the x-axis
			SmartDashboard::PutNumber(“Recursive Y-Axis Average:", ((yAcceleration*0.1) + (0.9*previousY)));
			//returns a recursive average for the y-axis
			SmartDashboard::PutNumber(“Recursive Z-Axis Average:”, ((zAcceleration*0.1) + (0.9*previousZ)));
			//returns a recursive average for the z-axis
			previousX = (xAcceleration*0.1) + (0.9*previousX);
			previousY = (yAcceleration*0.1) + (0.9*previousY);
			previousZ = (zAcceleration*0.1) + (0.9*previousZ);
			Wait(kUpdatePeriod); // Wait a short bit before updating again
		}
	}
};

START_ROBOT_CLASS(Robot);
```

