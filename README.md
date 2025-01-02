# Study-on-Platooning-Traffic-Light-Recognition-and-PID-Based-Path-Control-for-Autonomous-Robots


## Introduction to the Project
We introduce the implementation of a path tracking for platooning autonomous driving robots. The system employs PID control, a feedback control mechanism, to ensure the robots remain on track.
Ultrasonic sensors are also utilized to measure the inter-robot distance, enabling adaptive speed adjustments for the following robot.

## System Design
<details>
<summary>PATH TRACKING USING PID CONTROL
</summary>
  
<blockquote>
Autonomous robots require steering control to follow a target path. Steering control is implemented using PID (Proportional-Integral-Derivative) control, a type of feedback control.



The control equation of the PID controller is as follows :
</blockquote>
  
![image](https://github.com/user-attachments/assets/53b92143-006d-44dd-91dd-78ab6afa712e)




<blockquote>
We adopt the optimized values for each PID control gain through a manual tuning process.
</blockquote>



![image](https://github.com/user-attachments/assets/49ee9f2a-8436-4067-a0fe-3238a50f65a1)


<blockquote>
Method for calculating error values with 8 LSA(Light Sensor Array) sensors arranged in a line for path tracking, where the measured illuminance values from each sensor are stored and utilized in a list format. These values nable the autonomous robot to follow the white line on the track.
</blockquote>


![image](https://github.com/user-attachments/assets/dfbabf92-5890-418a-b21d-0e1ec0807f47)


<blockquote>
th and sensorvalue[i] denote the target value and the illuminance value measured by the LSA sensor i, respectively. 
The target value th indicates the value of the white line on the track measured by the robot's sensors. The error value using the average of the leftmost two sensor values is represented by Equation (2), the error value using the average of the center two sensor values is represented by Equation (3), and the error value using the average of the rightmost two sensor values is represented by Equation (4).

The manipulation amount is calculated according to the PID control formula in Equation (1). Through this formula, three manipulation amounts for each error value are generated, and the movement of the robot is delicately controlled so that the track may be accurately driven. 
</blockquote>


![image](https://github.com/user-attachments/assets/e51637e4-2f90-44bc-a179-b851dc8fb183)


<blockquote>
Algorithm 1 describes a control algorithm designed to ensure the stable driving of an autonomous robot along a track. This algorithm dynamically controls the robot's direction and adjusts the turning intensity for left and right turns based on data collected from LSA sensors mounted on the robot.
</blockquote>

</details>


<details>
<summary>PLATOONING</summary>
<blockquote>
In platooning, maintaining a safe distance between robots is essential for collision avoidance and smooth driving, requiring the following robot to respond appropriately to sudden speed changes of the leading robot.
</blockquote>

![image](https://github.com/user-attachments/assets/55c0791c-54d2-47cf-b9c2-281a30e75d5f)


<blockquote>
The core of this algorithm is to measure the distance between robots and speed adjustment based on this distance.
  

First, the distance between the following robot and the leading robot is measured in real-time using the ultrasonic sensor (line 1). 
If the distance becomes less than the minimum safe distance of 35 cm, the 
speed is reduced to about 0.12 m/s to maintain the distance, and if the distance becomes less than 27 cm, the robot is designed to stop (lines 4-8). 
When the distance between the robots exceeds 35 cm, the speed of the following robot is increased to about 0.17 m/s to maintain the 35 cm distance, enabling swarm driving (lines 10-11).
</blockquote>
</details>

<details>
<summary>TRAFFIC LIGHT RECOGNITION</summary>
<blockquote>
The autonomous robot is equipped with a camera to recognize traffic lights and respond accordingly, using a CNN-based image classification model. The model was trained with a total of 2 classes, using 1,500 Red and 1,500 Green images as training data. The training data was split into training and validation sets at an 8:2 ratio, while the test data consisted of 446 images in total, with 224 Red images and 222 Green images.
</blockquote>
</details>

## Experimental Methods


<details>
<summary>EXPERIMENTAL TOOLS</summary



<blockquote>
These are the experimental tools for integrating and validating the previously designed autonomous driving and platooning systems.
</blockquote>



![image](https://github.com/user-attachments/assets/93bd72bd-5225-4ef8-bed6-356575de322c)



<blockquote>
The leading robot(a) and the following robot(b). The following robot is equipped with an ultrasonic sensor at the front to measure the distance from the leading robot. An LSA sensor used to track the line while driving is also mounted at the front, which serves to detect the position of the line so that the robot can accurately follow the path.
</blockquote>


![image](https://github.com/user-attachments/assets/a53b05e8-275c-450e-841e-aa822c8addb8)


<blockquote>
Figure shows the experimental track for confirming the path tracking and platooning of the autonomous driving robot proposed in this study. 


The green line and the red line indicate the starting point of the leading robot and the starting point of the following robot, respectively. The yellow line indicates the point at which to stop to recognize the traffic light and the blue line indicates the slow-speed zone
</blockquote>


![image](https://github.com/user-attachments/assets/b7321b63-9072-4c34-be42-6a07cb3fdf7f)


<blockquote>
The robots are equipped to recognize traffic lights and control their movement accordingly by setting up two types of traffic lights (circular and rectangular). The traffic lights are operated by detection sensors.
</blockquote>
</details>

## Experimental Results
<details>
<summary>PATH TRACKING USING PID CONTROL
</summary>

  
![image](https://github.com/user-attachments/assets/15571a60-b8f4-4936-ac4f-ab1213c5ecbc)

<blockquote>
We use optimized PID control gain values obtained through a manual tuning process for both the leading and following robots. This table shows the optimized control gain values for the leading and following robots. These values are adjusted based on the characteristics of each robot and the driving environment to ensure stable driving.
</blockquote>
</details>

<details>
<summary>PLATOONING
</summary>

![image](https://github.com/user-attachments/assets/efd1b402-4652-4ab5-bc77-1ec30c8a76b9)


<blockquote>
Figure shows the robots maintaining their distance when Algorithm 2 is applied in practice. When the leading robot stops to wait for a traffic light, the following robot, which was trailing, stops while maintaining a safe distance. This visually demonstrates the process of platooning while maintaining the distance between the robots.
</blockquote>  
</details>

<details>
<summary>TRAFFIC LIGHT RECOGNITION</summary>


![image](https://github.com/user-attachments/assets/c0d76981-3e0d-427b-8581-4304376843b7)

<blockquote>
To evaluate the performance of the model, we measured the accuracy for training data and test data, and the results are as follows. In particular, the accuracy of this model is 95.96%. 
This confirms that the CNN-based image classification model can accurately identify traffic lights in real-time and appropriately reflect this information in the behavior of the autonomous robot.
</blockquote>
</details>

<details>
<summary>COMPREHENSIVE RESULTS</summary>

![image](https://github.com/user-attachments/assets/2147a161-9494-406f-8629-5c6659e7f2d8)


<blockquote>
Figure6 and Figure7 show data comparing the leading robot's route tracking before and after the application of PID control, respectively. 
The x-axis represents the time taken by the robot to complete two laps of the track, and the y-axis shows error2 in the path tracking and platooning system design using PID control. 




As seen in the graph, in the case without PID control, the error value fluctuates sharply without a consistent pattern, indicating unstable driving. This shows that the robot 
is unable to accurately track the white line in both the straight and corner sections. Also, there was an issue where the robot would deviate from the track, requiring the robot to be moved 
back onto the track. Therefore, it can be seen that the driving without PID control is more time-consuming and inefficient. 


When PID control is applied, the error value remained 
relatively constant, and it is found that the robot followed the white line well without any sudden change in the straight line section. In the corner section, the robot briefly deviated from 
the white line but quickly returned to it, demonstrating stable driving. This indicates that the PID control is functioning effectively.
</blockquote>


![image](https://github.com/user-attachments/assets/39ff514e-3b8c-493b-8801-fa2e315f6ef1)


<blockquote>
Figure shows the two robots starting simultaneously in the experiment, maintaining a safe distance while driving and stopping. In particular, it is confirmed that the following robot 
stops without collision even when the leading robot stops in front of the traffic light. This demonstrates that the system's autonomous driving and platooning functions work 
successfully in the experimental environment.
</blockquote>
</details>  


## Project Results Video 
[![Watch the video](https://img.youtube.com/vi/KbpQ3JgK9nE/0.jpg)](https://youtu.be/KbpQ3JgK9nE)


Clicking the image will take you to the YouTube page where you can view the result video.
