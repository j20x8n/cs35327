java c2024-2025 AVDC UAS Modelling and Simulation Assignment
Centre for Autonomous and Cyber-Physical Systems, SATM
Introduction
This is an individual assignment comprising a report and accompanying computer (software)
codes on dynamics and control, design and performance analysis of UAS. This assignment
handout consists of 11 pages. Submission is on Canvas, and for the deadline refer to the
module's Canvas site as normal.
The things you will (hopefully) gain are as follows:
1. Evaluate and implement an example UAV model in terms of their aerodynamic, control,
mass and inertia characteristics. Appraise and critically compare the resultant motion.
2. Distinguish the requirements for model testing, verification and validation, and
demonstrate their application to an UAV model.
3. Communicate and present results of individual work.
In this assignment you are asked to develop and analyse a high-fidelity nonlinear model of a
flying wing UAV; example of the UAV is given in Fig. 1 for the illustration purposes. The
small fixed-wing UAV has two control surfaces, elevons, and they operate both as ailerons and
elevators, and it has a brushless pushing DC electric motor to produce thrust.
The simulation model should contain the equations of motions, the aerodynamics model, the
propulsion model, the actuator model, environment model and control. All parameters required
to build this model are provided in the Appendix.
Fig. 1. Example of flying wing UAV1
1 https://flightory.com/2022/12/03/stingray-new-fpv-flying-wing-design/
2
The assignment comprises three sections, namely, modelling, trimming/linearization/stability
analysis and control. Details for the assignment are given in the following paragraphs.
The work must be presented as follows:
• A pdf document (assignment report), which provides the answers with supporting
plots/figures to each of the questions of the following paragraphs.
• A folder containing all MATLAB/Simulink codes used to answer the questions.
The evaluation criteria for the final assignment are the following
• Quality of the results (25%)
• Quantity of the results (25%)
• MATLAB/Simulink code quality and clarity (25%)
• Assignment report quality (25%)
3
Part 1 - Modelling (40%)
The first task of the assignment is to build the simulation model of the UAV system using
MATLAB/Simulink. The system considered in this assignment will include:
• The equations of motion (6-DOF equation, navigation equation, kinematic equation).
• The model of aerodynamic loads.
• The propulsion model, incl. motor model.
• The environment model (wind model and atmosphere model).
• The actuator models.
Question 1: Model Conceptualization (2%)
Develop a schematic diagram of the system (conceptual model) and explain the interactions
between the sub-systems.
Hints:
1) No MATLAB/ Simulink code needed.
2) The schematic diagram means a high-level block diagram representing relationship between
the substantial subsystems described above.
Question 2: Flight Dynamics (3%)
Most aerospace systems use the same equations of motions including 6-DOF equation, the
kinematic equation, and the navigation equation. It means that you can utilize the same model
structure discussed during the module. Before development the simulation model, please,
explain the equation of motion in details.
Hint:
No MATLAB code needed.
Question 3: Modelling (10%)
Mathematical models of sub-systems, such as the aerodynamics model, the actuator model, the
propulsion model and control for the UAV are provided in the Appendix. Using the equations
of motion and provided mathematical models, please, develop the simulation model of the
UAV using MATLAB/Simulink and explain it.
Hints:
1) You may include all parameters needed to build this model in a separated MATLAB file
named “UAV_data.m” similar to the MBD Exercises.
2) While building the model, you can utilize “Aerospace Blockset” from the Simulink Library.
3) When you compute arctangent function, please use the function named “atan2” instead of
“atan”.
4
4) Solver setting: Go to “simulation” tab -> “model configuration parameter” -> “Solver”
 Please set the solver as follows:
 - Type: Fixed-step
 - Solver: ode4(Runge-Kutta),
 - Fixed-step size: Step_Size (this value is already defined in “Sim_Parameters.m”)
5) Initialization setting: Go to “File” tab -> “Model Properties” -> “Callbacks” -> “InitFcn*”
 Please set the following initializations:
clc ;
clear all ;
close all ;
UAV_Data ;
Sim_Parameters ;
Question 4: Model Verification (25%)
After building the model, please verify the simulation model using the model verification
techniques, which were introduced within the module.
Hint:
Verification techniques are the following: tracing, comparing outputs of simulation models
and outputs of mathematical models, checking the simulation model using prior knowledge.
In particular, a simulation model using prior knowledge should be checked as follows:
1. Check whether control inputs produce the desired motion
2. Check the longitudinal and lateral modes.
5
Part 2 - Trimming/Linearization/Stability Analysis (50%)
The second task of the assignment is to find trim solutions at given operating conditions and
then get linearized models at the trim conditions found. Additionally, it is required to assess
the stability of the system.
Question 1: Process of Trimming and Linearization (5%)
Explain the process of trimming and linearization, incl. trimming constraints; discuss why we
need these additional constraints:
1. What is linearization from the mathematical point of view?
2. Why do we need Trimming and Linearization?
3. What is the trim point from the point of view of the governing equation?
4. Why do we need to apply constraints?
Hint:
No MATLAB/Simulink code needed.
Question 2: Finding Trim Solutions and Trim Analysis (20%)
Build the simulation model for trimming and the simulation model for checking the obtained
trim solutions.
a) Find a trim solution at the operating condition airspeed 𝑉 = 15 𝑚/𝑠 and h = 0 𝑘𝑚
(Altitude). Verify the trim solution found using the simulation model for checking trim
solutions.
b) Find trim solutions at the fixed altitude h = 0 𝑚 and various speeds 𝑉 = [15,
30, 45,60] 𝑚/𝑠. In this case, determine the trim angle-of-attack (i.e.,
e e e
= atan 2 , (w u )
), the
trim pitch control elevator deflection (i.e., 𝛿𝑒
), and the trim throttle (𝛿𝑡ℎ
). Discuss patterns of
these parameters as speed increases. Also, please, discuss the reason behind this behaviour.
c) Find trim solutions at the fixed airspeed 𝑉 = 15 𝑚/𝑠 and various altitudes as h =
[0,1, 2, 3, 4] 𝑘𝑚. In this case, determine the trim angle-of-attack (i.e.,
e e e
= atan 2 , (w u )
), the
trim pitch control elevator deflection (i.e., 𝛿𝑒
), and the trim throttle (𝛿𝑡ℎ
). Discuss patterns of
these parameters as Altitude increases. Also, please, discuss the reason behind such a behaviour.
Hints:
1) When you find trim solutions, the thrust needs to be included as the control input in order to
maintain a constant speed. Therefore, the control inputs are 𝛿𝑡ℎ
and 𝛿𝑒
.
2) Variation of trim solutions according to changes in airspeed and altitudes are closely related
to variations of the dynamic pressures. Note that the dynamic pressure is defined with
2 Q V = (1/ 2)
, where
V
is代 写program、Java/python
代做程序编程语言 the speed and

is the air density.
3) Initialization setting: Go to “File” tab -> “Model Properties” -> “Callbacks” -> “InitFcn*”
6
 You can set the following initializations similar to the MBD Exercises:
UAV_Data;
Question 3: Numerical Linearization (10%)
Build the simulation model for linearization. Perform numerical linearization at the operating
condition 𝑉 = 15 𝑚/𝑠 and h= 0 𝑚. Determine the linear time invariant (LTI) model of the
longitudinal motion and the LTI model of the lateral motion.
Hints:
1) For UAV systems, the state vector and the input vector of the longitudinal motion are
 , , , 
T
lon x = u w q 
and 𝑢𝑙𝑜𝑛 = [𝛿𝑒
].
2) For UAV systems, the state vector and input vector of the lateral motion are
 , , , 
T
lat x = v p r 
and 𝒖𝑙𝑎𝑡 = [δ𝑎
].
3) Initialization setting: Go to “File” tab -> “Model Properties” -> “Callbacks” -> “InitFcn*”
Please set the following initializations:
UAV_Data;
Question 4: Stability Analysis (15%)
Determine the dynamics modes of the longitudinal and lateral motion. Discuss the dynamic
characteristics of these modes in the terms of the stability, the natural frequency, and the
damping ratio (plot zero-poles map). Identify these modes in the state responses.
Hint:
You can use MATLAB commands named “eig” and “damp”.
Part 3 - Implementation of Control Laws (10%)
Control is an important element within the remit of aerial vehicle design. In this section, you
are required to implement the provided control laws to the simulation model.
Question 1: Implementing Control Law (10%)
In the UAV, the autopilot system consists of the longitudinal controller and the lateral
controller, and the roll controller. The controller has three parts: longitudinal controller, lateral
controller and speed controller. The longitudinal controller includes pitch rate control, pitch
angle control and height control and the lateral controller includes roll rate control, roll angle
control and course angle control, while the speed controller only controls the airspeed of the
aircraft. The proportional (PID)-control type controller is widely used for these types of the
controllers.
7
The detailed information on the autopilot is provided in the Appendix. Implement the control
laws to the nonlinear simulation model. Evaluate the responses of the UAV under different
commands, namely, airspeed, course angle and altitude. In this case, the initial conditions are
set to be the trim solution at the operating condition 𝑉 = 15 𝑚/𝑠 and h= 0 𝑘𝑚. Is the tuning
of the coefficients sufficient? Does the flight control system require additional modifications?
If yes, perform coefficient tuning to improve system performance.
Hint:
The trim control inputs need to be added to the control inputs from the control system.
8
Appendix
A. Geometric, mass and inertia characteristics of the UAV
The geometric and mass characteristics are provided in Table 1.
Table 1
Parameter Value
Aspect Ratio (AR) 3.68
Chord (c) 0.25 m
Reference area (S) 0.22 m2
Mass (m) 1 kg
Wing span (b) 1 m
Moment of inertia is provided in Table 1.
Table 2
Parameter Value [kg ∙ m2
]
𝐼𝑥𝑥 0.023
𝐼𝑦𝑦 0.02
𝐼𝑧𝑧 0.033
𝐼𝑥𝑧 ,𝐼𝑧𝑥 0.006
𝐼𝑦𝑧,𝐼𝑧𝑦,𝐼𝑥𝑦 ,𝐼𝑦𝑥 0
B. Aerodynamics Model
The force and moment coefficients are represented with the following model
𝐶D = 𝐶D0
+ 𝐶Dα
α + 𝐶Dα
2
α
2 + 𝐶Dβ
β + 𝐶D
β
2
β
2 + 𝐶Dδ𝑒
δ𝑒
, (1)
𝐶L = 𝐶L0
+ 𝐶Lα
α + 𝐶Lq
c
2𝑉
𝑞 + 𝐶Lδ𝑒
δ𝑒
, (2)
𝐶Y = 𝐶Y0
+ 𝐶Yβ
β + 𝐶Yp
b
2𝑉
𝑝 + 𝐶Yr
b
2𝑉
𝑟 + 𝐶Yδ𝑎
δ𝑎
, (3)
𝐶m = 𝐶m0
+ 𝐶mα
α + 𝐶mq
c
2𝑉
𝑞 + 𝐶mδ𝑒
δ𝑒
, (4)
𝐶l = 𝐶l
0
+ 𝐶lβ
β + 𝐶lp
b
2𝑉
𝑝 + 𝐶lr
b
2𝑉
𝑟 + 𝐶lδ𝑎
δ𝑎
, (5)
𝐶n = 𝐶n0
+ 𝐶nβ
β + 𝐶np
b
2𝑉
𝑝 + 𝐶nr
b
2𝑉
𝑟 + 𝐶nδ𝑎
δ𝑎
(6)
where the parameters
V
is the UAV speed. 
and

represent the angle-of-attack and the
side-slip angle, which are defined as
9
1 1 tan , sin w v
u V
 
− −    
= =        
. (7)
The parameters 𝐶(∗)
are the aerodynamic coefficients, which are given in the Table 3. δ𝑒
, δ𝑎
denote the elevator and aileron deflection of the UAV, respectively. Due to the particular
structure of the flying wing UAV, there is no rudder. Yaw control is implemented via aileron.
δ𝑒
, and δ𝑎
can be decoupled into expressions of left and right elevon deflections δ𝑒𝑙𝑣𝑙
and
δ𝑒𝑙𝑣𝑟
by the following equation.
[
δ𝑒
δ𝑎
] = [
1 1
−1 1
] [
δ𝑒𝑙𝑣𝑙
δ𝑒𝑙𝑣𝑟
] (8)
The aerodynamics coefficients are given in the Table 3.
Table 3. Aerodynamic force coefficients
Parameter Value Parameter Value
𝐶D0
0.0208 𝐶m0
-0.0112
𝐶Dα
0.0084 𝐶mα
-0.2625
𝐶D
α
2
1.3225 𝐶mq
-1.8522
𝐶Dβ
-0.0001 𝐶mδ𝑒
-0.2845
𝐶D
β
2
0.0796 𝐶l
0
0
𝐶Dδ𝑒
0.2 𝐶lβ
-0.0345
𝐶L0
0.0389 𝐶lp
-0.3318
𝐶Lα
3.2684 𝐶lr
0.0304
𝐶Lq
6.1523 𝐶lδ𝑎
0.182
𝐶Lδ𝑒
0.7237 𝐶n0
0
𝐶Y0
0 𝐶nβ
0.0252
𝐶Yβ
-0.1285 𝐶np
0.002
𝐶Yp
-0.0292 𝐶nr
-0.0192
𝐶Yr
-0.0355 𝐶nδ𝑎
-0.0102
𝐶Yδ𝑎
0.0299
10
C. Aerodynamic Forces and Moments
The aerodynamic forces (Drag, Lift, Side force) are given by the equations:
𝐹𝐷 = QS𝐶D, 𝐹𝐿 = QS𝐶L
, 𝐹𝑌 = QS𝐶𝑌
. (9)
The aerodynamic moments (pitch, roll, yaw) are given by the equations
𝑚 = QSc𝐶𝑚, 𝑙 = QSb𝐶𝑙
, 𝑛 = QSb𝐶𝑛
(10)
where Q is the dynamic pressure, which is given by Q = (1/2)𝜌𝑉
2
.
D. Propulsion Model
In general, the thrust generated by the propeller depends not only on the rotating speed of the
propeller but also on the aircraft airspeed. Since the airspeed of the UAV considered in the
assignment is relatively small, only the influence of the rotating speed on the thrust is
considered to simplify the analysis. The thrust and the counter torque produced by the propeller
is described with the following equation
𝑇 = 𝐾𝑇𝑁
2
, (7)
𝑀 = 𝐾𝑀𝑁
2
. (8)
Where 𝐾𝑇 = 2.015 × 10−6 Kg · m, 𝐾𝑀 = 2.444 × 10−10 Kg · m2
.
E. Motor Model
The motor model includes the relationship between throttle and rotating speed by a simplified
linear dependency:
𝑅𝑃𝑀 = 7000 + 20000 𝛿𝑡ℎ
, (9)
where 𝛿𝑡ℎ
is the throttle command. The throttle has a dead zone below 0.1.
The motor is a first-order system with the time constant 𝜏 = 0.19 .
F. Actuator Model
The actuator system of each channel (roll, pitch, and yaw) is modelled as the second order
system as
𝛿
𝛿𝑐
=
𝜔𝑎𝑐𝑡
2
𝑠
2 +2𝜁𝑎𝑐𝑡𝜔𝑎𝑐𝑡𝑠+𝜔𝑎𝑐𝑡
2
, (10)
where the parameters 𝜔𝑎𝑐𝑡 and 𝜁𝑎𝑐𝑡 are the natural frequency and the damping ratio of the
actuator system; 𝜔𝑎𝑐𝑡 = 9.774, 𝜁𝑎𝑐𝑡 = 0.801.
G. Autopilot Model
The block diagram of the flight control is given in Fig. 2.
11
Fig. 2. Flight control system diagram.
Table 4. Flight control system coefficients
Parameter Kp Ki Kd
Longitudinal Pitch rate 0.3 7.50 0.0591
Pitch angle 8.2978 0.2536 0.1088
Altitude 0.6879 0.2373 0.1282
Lateral Roll rate 0.2631 5.5033 0.047
Roll angle 22.2973 0.0329 0.7683
Throttle Course angle 1.02 0.0011 0
Airspeed 1.4665 0 0.2171

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
