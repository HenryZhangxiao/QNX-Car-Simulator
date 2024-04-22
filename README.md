<h1 align="center">
    QNX Car Simulator
</h1>

## Introduction

RTOS plays an important role in automotive development by enabling critical features in a car to run with minimum latency.
An RTOS implementation into a car ensures the scheduler will execute processes within a fixed predetermined amount of time.
This is critical for components such as the brakes, airbags, etc.
We have implemented the simulation of the basic essential functions of a car.
The specific implementation for this RTOS system will entail the steering, throttle, brake, indicators, airbags, and engine state functions of the car

A demonstation of this project can be [found here](https://www.youtube.com/watch?v=vymPq745m40)

#### Table of Contents
- [Softwares used](#softwares)
- [Methodology](#methodology)
- [Message Structures](#message-structures)
- [Steering](#steering)
- [Indicators](#indicators)
- [Throttle and Brakes](#throttles-brakes)
- [Engine](#engine)
- [Future Considerations](#future)
- [Authors](#authors)

<br></br>


## Softwares used <a name="softwares"></a>

- C
- QNX SDP 7.1
- mkqnximage
- Git/GitHub

<br></br>


## Methodology <a name="methodology"></a>

Our car simulation implements every functionality of the car as a separate process.
The reason behind this design decision was to separate each function in true microkernel fashion where functions do not have an interdependency. Functional separation also gives us the freedom to add more functionality later and provide an ability to interface with an external GUI.
For the architecture of our car simulation, the engine will act as the server and every functionality will act as a client.

![image4](https://user-images.githubusercontent.com/44578113/233807651-7f07d72c-71d9-4417-a053-8c8256b39230.png)

<br></br>


## Message Structures <a name="message-structures"></a>
![image](https://user-images.githubusercontent.com/44578113/233807887-7f5ba43b-01c3-4a2d-861c-89a5eb4428df.png)

<br></br>


### Steering <a name="steering"></a>
For the steering functionality, we decided to base it off of the relationship between the turn range of the steering wheel and the car’s turning angle.
For the steering wheel, we set up the range to be from 0° to 180°.
The angles from 0° to 89° represent a turn to the left, 90° means the car is remaining straight, 91° to 180° means the car is turning right. If the user inputs anything below 0°, the angle will be set to 0°. The same logic applies for any input above the maximum turn angle of 180°, since the angle would be set to 180° if an input of 180° or above is provided for the steering. 

The direction the car goes based on the angle provided by the steering toggle message is calculated as such: 

CarAngle = *| 90 - steeringToggleMessage.angle |*

For example, if steering_toggle_msg.angle = 45°, the car will be turning left at a 45° angle. Another example, if steering_toggle_msg.angle = 180°, the car will be turning right at a 90° angle.

![image](https://user-images.githubusercontent.com/44578113/233812331-bdc6dad6-7638-4344-a7bd-d1bf785a6ac5.png)

<br></br>


### Indicators <a name="indicators"></a>
A car has two indicator lights, one for the left side and one for the right. The indicator code works as a toggle where each side can be turned on/off independently

<br></br>


### Throttle and Brakes <a name="throttles-brakes"></a>
For the throttle and brakes, the functionality works the same for both. We are using a scale of 0 to 100 which represents the pressure in which the driver would be pressing on the gas pedal or the brake pedal. Depending on the pressure given into the gas or brake pedal, we multiply that input by a scale of 20 rpm, which will be added to or subtracted from the current rpm value

We have also set a minimum and maximum rpm level that the user cannot go below or above

<br></br>


### Engine <a name="engine"></a>
The engine toggle serves as a toggle to shut off the engine (server).

<br></br>


## Future Considerations <a name="future"></a>
In terms of future considerations, we would have liked to implement thread priority for airbags and brakes as that would be important for the car to have certain safety functionalities prioritized over others. We would have also liked to have implemented and separated the transmission states - Park, Reverse, Neutral, and Drive. 

Finally, our goal was to implement a GUI, however, we did not have the correct licenses to be able to implement the GUI. Alternatively, it would have been an even more interesting project if we could have run the project on a physical board with physical buttons/knobs, however this was not possible due to geographical limitations for our team

<br></br>


## Authors <a name="authors"></a>
Henry Zhangxiao

Siddharth Natamai

Danna Liu

<br></br>

