##Object Usage
In object-oriented programs (OOP), objects are basically objects like that of the real world, and thus have certain behaviors and characteristics. Characteristics of an object in OOP include any variables or other objects that are declared in the class that the object is written in. Behaviors of an object are methods that the object contains in its class code.

We will use the Jaguar class from the WPI library to help explain this section. Click [here](http://mililanirobotics.org/documentation/electrical/WPILib2015C++/classJaguar.html) to view it.

###➠ Defining Objects
Defining objects is a similar to defining variables, but instead the data type is replaced by the name of the object. After the object name comes the name that you assign to the address location of the object. In terms of the Jaguar class, a Jaguar object is defined as:
```c++
Jaguar jag1;
Jaguar jag2;
Jaguar example;
```
Remember that each Jaguar object that you create is a different instance of the object and that different spaces in memory are created for instance variables of each Jaguar object. The name you gave to a Jaguar object is the only thing you have to distinguish between Jaguars.

###➠ Instantiating Objects
Instantiating an object is quite different from defining a variable. When instantiating an object, you must use the `new` operator. Followed by the `new` operator is the object’s constructor signature. An object’s constructor signature may look like this:
```c++
Jaguar (UINT32 channel)
```
As you can see the object name is displayed along with some code inside parentheses.  The code inside the parentheses is called a parameter. Parameters are where you pass data into the object so that the object can use it. Notice that data in parameters are separated by commas. In the above case, the object constructor asks you to input a float and a channel number. So an example instantiation would look something like the following:
```c++
jag1(1)
```
Where `1` is the number of a `UINT32 channel` (the PWM OUT port the jaguar occupies on the digital sidecar).

Object classes often have multiple constructors which ask for different sets of parameters. In the case of the [Solenoid](http://mililanirobotics.org/documentation/electrical/WPILib2015C++/classSolenoid.html) class, here are the following constructors for a Solenoid object.
```c++
Solenoid (uint32_t channel) //Constructor using the default PCM ID
Solenoid (uint8_t moduleNumber, uint32_t channel) //Constructor that specifies the PCM ID.
```
You should see that the only thing different is the parameters that must be called. The first calls for the PCM channel only (assumes the  PCM ID as `0`). To call the first constructor after defining `sol1`, you would type:
```c++
sol1(1)
```
which means `sol1` is assigned to PWM port `1` on the PCM and is automatically assumed to be on the PCM ID of `0`.

Because the roboRIO can support more than one PCM, anything connected a PCM with an ID that is not `0` will need to use the second constructor.

###➠ Using Methods
In programming, objects alone do no more than they do in reality. Simply stating “the Jaguar exists!” will not make your robot move, nor will merely declaring it in your code make anything happen.

The real work is done through methods, a unique set of commands that each object has. These are noted by a `.` after the name of a particular object and are always followed by `()`, though often there are some values passed into the parentheses. In the Jaguar class, for example, one might see the following code fragment:
```c++
jag1.Set(0.5);
```
The name of the object is `jag1`, which has previously been declared to be a Jaguar. The method is `Set`, which, as one might expect, sets the speed of the motor. The `0.5` inside the parentheses is called the parameter, which varies depending on the method used. Here, it is a float value from `-1` to `1`, inclusive, but often you must pass an int, bool, or even another object as a parameter. For object-specific information on methods and parameters, see the section on that particular object or use the WPI Library.

Note that just as each object will have multiple methods, different objects can have methods of the same name and may or may not do different things. The Victor class, for example, also has a Set method that functions exactly the same, but the Relay class takes an entirely different data type and functions purely as an on/off switch.

