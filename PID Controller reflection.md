# PID Controller for the Udacity Simulator

This project consists of a c++ implementation of PID controller to control the steering angle of a car using the Udacity simulator. The main goals of this project is to develop a c++ PID controller that successfully drives the vehicle around the track (Udacity simulator). Figure 1 depicts the car being controlled by the PID controller. 


## PID 

The PID (Proportional, Integral and Derivative) controller is a shut circle controller broadly utilized by the business. It figures the framework input variable from the mistake e(t) between the ideal set point and the framework yield (process variable). The control reaction (framework input) is determined by applying the corresponding, subordinate and vital increases over e(t). 

For this task, the PID controller is utilized to control the guiding point from the ''cross track blunder'' e(t) (vehicle good ways from the track community). In this way, the framework input is the directing edge, the yield is the vehicle good ways from the inside and the setpoin it zero (nearest to the middle as could be expected under the circumstances).

![equation](http://latex.codecogs.com/gif.latex?%5Calpha%20%3D%20-K_pe%28t%29%20-K_d%5Cfrac%7Bde%28t%29%7D%7Bdt%7D%20-%20K_i%5Csum%20e%28t%29)

### Kp (Proportional Gain)

The Kp gain results into a corresponding control reaction. With regards to this task, it implies that the cow input is in relation to the Cross Track blunder. In any case, the corresponding control alone outcomes into a barely steady framework in light of the fact that the vehicle will never unite to the set point, it will somewhat overshoot. Moreover, expanding the estimation of Kp will cause the vehicle to respond quicker however it will likewise waver more around the inside path (set point). This [video](https://youtu.be/ZL0ugIRzb34) shows the oscillation of the car trajectory using a proportional controller. 

### Kd (Derivative Gain)

The Kd gain considers the rate change of mistake and attempts to carry this rate to zero. The subordinate addition supplements the relative yield by lessening the overshoot, it mains objective is to leveling the vehicle direction. This [video](https://youtu.be/s39sRH-E5jc) presents the smoothed trajectory of the car using a proportional-derivative controller. 


### Ki (Integral Gain)

The Ki gain diminishes the tenacious mistake, for example the aggregated blunder. The indispensable addition encourages the controller to manage the ''deliberate predisposition'' issue witch prompts a methodical blunder. The Ki increase should assist with evacuating the leftover blunder to surmised the vehicle close to the focal point of the track.This [video](https://youtu.be/-K5XIo5vCzM) illustrates the car following the lane center using a complete PID controller. The Ki gain diminishes the tenacious mistake, for example the aggregated blunder. The indispensable addition encourages the controller to manage the ''deliberate predisposition'' issue witch prompts a methodical blunder. The Ki increase should assist with evacuating the leftover blunder to surmised the vehicle close to the focal point of the track.

## PID Tunning

The PID tuning for this venture followed a blend of manual and programmed tuning draws near. To start with, because of the reenactment time (~90 seconds) required to assess a lot of PID gains, we chose to initially follow a manual way to deal with discover the increase orders. We watched the accompanying significant degrees for the PID gains:

* Proportional: order of 0.1
* Integral: order of 0.001
* Derivative: order of 0.0001


The second step it to use the [Twiddle Algorithm](https://martin-thoma.com/twiddle/) to fine tuning the PID gains. We used the gain orders we had previously manually found to help the Twiddle algorithm to converge faster by setting the tiwdle starting vectors to: 

* Initial PID Vector: {0.01, 0, 0.0007} (values manually tunned)
* Potential changes: {.1,.001,.0001}

The twiddle calculation assesses each new arrangement of boundaries and checks if the mistake is littler. On the off chance that the mistake is more prominent, the potential change vector is changed and another arrangement of boundaries is endeavored. Be that as it may, on account of the various corners range of the track, we need to assess the PID controller into a since quite a while ago run, so as to test if the arrangement of boundary (gains) is all around adjusted for the track, and not just for a little subset. This methodology makes the investigation truly long; 40 cycles took very nearly 60 minutes; we have chosen to stop the calculation after 100 emphasess.

The final PID controller successfully drives the car around the track without pop up onto ledges or roll over any surfaces that would otherwise be considered unsafe (if humans where in the vehicle). The file PID parameters are shown below:

* Kp: 0.11
* Ki: 0.00415711
* Kd: 0.00087019

This [video](https://youtu.be/OoGZPebVSMg) shows the car driving around the corner with the PID controller set with the parameters presented above. 

