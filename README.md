# Simulink

I did this project during the embedded lab. 
The purpose of this assignment is to controll the robotic arm's five servo 
with 5 switches and 2 buttons on the the Zedboard
By turning on the corresponding switches will activate certain servo motor on the arm 
and by pressing the up and down button, the servo motor will changes angles

In the simulink subsystem and in the configurablePWM 
A pwm signal generater is being created by compairing two HDL counter (setCounter & HDL_pwm)

The HDL_pwm counter is set at 20ms period since the count to value is set to 1000000 and the the 
frequency of the board is 5000000, dividing the two numbers will give us 0.2.

The setCounter will generate the signal that will be less than 20ms, in this case the maximum angle 
the servo can reach is 180 degree and 0 degree is the least and we would like the arm to start from 90 
degrees. Count from value is correspond to the 0 degree angle due to the calculation:
Sinec 0.6 ms is corresponding to 0 degree and 1.5 ms = 90 degrees; 2.4 ms = 180 degrees. 

0.6 ms = 0.6 x 50,000 cycles = 30,000 cycles (countfrom value) 
1.5 ms = 1.5 x 50,000 cycles = 75,000 cycles (initial value) 
2.4 ms = 2.4 x 50,000 cycles = 120,000 cycles (Count to value)
Since the assignment required "the servo traverses its entire range (between 0-180 degrees(0.6ms to 2.4ms)
in 15 clock cycles, 
thet step value can be calculated with (120,000 - 30,000)/15 = 6000 (step value)

The compare to constant make sure that when the counter reach the maximum or minimum degree, it will not 
reset back to 90 degree or the initial value of the counter.

// IN the subsystem, 
Since there are 5 servo motor, the configuratbel PWM block has been copied 5 times, each outputs 
represents an servo motor. 
