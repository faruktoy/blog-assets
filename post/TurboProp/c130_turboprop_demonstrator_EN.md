# C-130, T56, R391 and Variable-Pitch Propeller Logic

## A Technical Study Through a 3D Turboprop Demonstrator Model

In turboprop engines, the real challenge is not merely making the engine spin. How engine power is transferred to the propeller, how propeller RPM is controlled, how blade angle changes, and how the governor system balances these variables must all be considered together. In large turboprop aircraft like the C-130, the propeller is not just a rotating thrust element — it is an active control system that transfers engine power to the air.

This article provides a technical examination of the T56 engine used in the C-130 family, the 54H60 propeller system, the R391 propeller geometry, constant-speed propeller logic, and how these concepts can be represented in a 3D turboprop demonstrator model.

The base 3D geometry used in this project was taken from the Cadly turboprop model. However, the software and electronics side was not left as a simple "prop-power lever" display; it has been transformed into a more instructional demonstrator with Condition Lever, Power Lever, AIR START animation, two different RUN modes selectable via toggle switch, servo-controlled blade angle movement, and propeller rotation represented by a DC motor.

<!-- VISUAL PLACEHOLDER: Photograph
     Description: General view of the 3D-printed turboprop demonstrator model
     SearchKeywords: 3D printed turboprop propeller pitch demonstrator model -->

---

## Engine and Propeller Logic in the C-130 Family

The C-130 family has been used with different engine and propeller combinations over many years. Classic models such as the C-130E/H use the Allison, now Rolls-Royce, T56 turboprop engine. Rolls-Royce describes the T56 as a "single shaft, modular design" turboprop engine. The same source states that the T56 contains a 14-stage axial compressor, 4-stage turbine, and two-stage reduction gearbox; that a propeller brake is located in the reduction gearbox; and that the system is linked to the power section through the torquemeter assembly. ([Rolls-Royce][1])

On the C-130J Super Hercules side, the Rolls-Royce AE2100D3 engine and Dowty/GE Aerospace R391 six-blade composite propeller system are used. Rolls-Royce states that the AE2100D3 is used in C-130J and LM-100J transport aircraft. ([Rolls-Royce][2]) The R391 is a modern propeller with hydraulic constant-speed, counterweight, reversible, and full-feathering capabilities. The Smithsonian source notes that the R391 has a six-blade composite structure and a diameter of approximately 4.115 m. ([National Air and Space Museum][3])

The fact that the 3D model in this project draws visual inspiration from the R391 does not mean it is a direct replica of a real C-130J cockpit control system. The R391 was chosen because it looks more modern and visually striking. The control logic, however, has been designed in software to convey the Power Lever, Condition Lever, governor, feather, ground stop, and air-start concepts seen particularly in the T56/54H60 system within the C-130 family.

<!-- TABLE: C-130 Family Engine and Propeller Comparison -->

| Feature | C-130E/H | C-130J Super Hercules |
|---|---|---|
| Engine | Allison/Rolls-Royce T56-A-15 | Rolls-Royce AE2100D3 |
| Engine type | Single-shaft turboprop | Free-turbine turboprop |
| Propeller | Hamilton Sundstrand 54H60 | Dowty/GE Aerospace R391 |
| Number of blades | 4 | 6 |
| Propeller diameter | ~4.11 m (13 ft 6 in) | ~4.115 m (13 ft 6 in) |
| Blade material | Aluminium alloy | Composite |
| Propeller features | Hydraulic constant-speed, feathering, reversing | Hydraulic constant-speed, counterweight, full-feathering, reversing |
| Engine control | Hydromechanical fuel control + TD system | FADEC (Full Authority Digital Engine Control) |
| Propeller RPM (takeoff) | ~1021 RPM | ~1020.7 RPM |

<!-- VISUAL PLACEHOLDER: Photograph
     Description: Allison/Rolls-Royce T56 engine and 54H60 propeller system
     SearchKeywords: Allison T56 engine 54H60 propeller C-130H -->

<!-- VISUAL PLACEHOLDER: Photograph
     Description: Dowty R391 six-blade C-130J propeller view
     SearchKeywords: Dowty R391 six blade propeller C-130J -->

---

## Constant-Speed Propeller Logic

One of the most critical concepts in turboprop systems is constant-speed propeller logic. In a constant-speed system, the goal is to keep propeller RPM close to a specific target value. When the engine wants to produce more power, the propeller tends to accelerate. The governor system detects this and changes the blade angle so that the propeller takes on more aerodynamic load. Thus, while engine power increases, propeller RPM is kept close to a constant value.

The C-130 flight manual states that propeller speed in the Flight Range is controlled by the propeller governing system to maintain constant RPM, and that in the Ground Range, blade angle is a function of throttle lever position. The same section explains that the low pitch stop prevents the blade angle from falling below approximately 23° within the Flight Range. ([Uniforce-SOG][4])

On the T56 side, 100% engine speed is approximately 13,820 RPM. The Lockheed Martin Service News source states that with a 13.54:1 reduction ratio, this corresponds to approximately 1,021 RPM on the propeller side. ([Lockheed Martin][5]) The R391 side also has a similar constant-speed character; the R391 type certificate data gives the takeoff propeller speed as 1,020.7 RPM and the maximum continuous propeller speed as 1,020.7 RPM. ([CAA][6])

The important conclusion here is: in the real constant-speed logic of the C-130 family, propeller RPM does not continuously increase when the Power Lever is advanced. During normal flight, RPM is kept close to a constant; what changes is primarily torque, fuel flow, and blade angle.

<!-- DIAGRAM PLACEHOLDER: Governor Operating Principle
     Description: Schematic diagram showing the constant-speed propeller governor's pilot valve, flyweight, and blade angle feedback loop
     SearchKeywords: constant speed propeller governor pilot valve flyweight schematic -->

<!-- GRAPH PLACEHOLDER: RPM vs Power Lever Position
     Description: Line graph showing that as Power Lever is advanced in a constant-speed system, RPM remains nearly constant while blade angle and torque increase
     Axes: X = Power Lever position (%) | Y₁ = Propeller RPM | Y₂ = Blade angle (°) | Y₃ = Torque (ft-lbs)
     SearchKeywords: constant speed propeller RPM torque blade angle vs power lever graph -->

---

## Blade Pitch, Blade Angle, and the Feather Concept

In this article, "propeller" refers to the entire propeller assembly, while "blade" refers to individual blade elements of the propeller.

Blade pitch or blade angle refers to the angle each blade takes relative to the airflow. At a low blade angle, the blade "bites" less air and the propeller turns more easily. At a high blade angle, the blade interacts with more air on each revolution and the propeller creates more aerodynamic load.

In general constant-speed propeller training, a low pitch / high RPM combination is used for takeoff, while a higher pitch / lower RPM combination can be used for cruise. The FAA training material also explains that a low-pitch/high-RPM setting is used for takeoff, and a higher pitch and lower RPM setting can be used after takeoff. ([Federal Aviation Administration][7]) However, in systems like the C-130/T56, this relationship cannot be read directly one-to-one from the Power Lever, because in the flight range, propeller RPM is kept close to a constant by the governor. ([Uniforce-SOG][4])

Feather is the position where the blades are brought more parallel to the airflow. In the event of engine failure or engine shutdown, feathering is used to reduce propeller drag. The R391 propeller system also has full-feathering capability. ([National Air and Space Museum][3])

<!-- TABLE: Representative Blade Angle Values Used in the Model -->

| Operating Region | Representative Blade Angle | Description |
|---|---|---|
| Low Pitch / Ground | ~0° – 5° | Propeller at minimum aerodynamic load |
| Flight Idle / Low Pitch Stop | ~23° | Minimum flight angle permitted by governor |
| Takeoff / Climb | ~23° – 35° | High power, increasing blade angle |
| Cruise / High Pitch | ~35° – 55° | High blade angle for cruise efficiency |
| Full Feather | ~93° | Blade parallel to airflow; minimum drag |

> **Note:** These values are not operationally valid control data. The model's purpose is to make blade angle behaviour visually and educationally understandable.

<!-- DIAGRAM PLACEHOLDER: Blade Angle Comparison
     Description: Side-by-side cross-section views of the same propeller blade in low pitch, cruise pitch, and feather positions
     SearchKeywords: propeller blade angle low pitch high pitch feather cross section comparison diagram -->

---

## Why Is Reverse Not Included Yet?

In real turboprop systems, reverse thrust is produced by moving the blade angle below zero or into the negative pitch region. The R391 type certificate data states that the propeller is of the variable-pitch, constant-speeding, feathering, and reversing type; and that beta control provides manual pitch selection for aircraft braking and ground manoeuvring. ([CAA][6])

However, the mechanical design of this 3D demonstrator model does not currently support the negative blade angle region. Therefore, although reverse mode is known in the software logic, it has not been implemented in the physical model. The current version of the model focuses on low positive blade angle, flight idle, climb/cruise representation, feather, and air-start/unfeather movements.

This has been accepted as a limitation of the model. If the mechanical linkage and servo travel range are revised in the future to support negative blade angles, the reverse region can be added as a separate display mode.

<!-- DIAGRAM PLACEHOLDER: Reverse Pitch Logic
     Description: Diagram showing the relationship between blade and airflow direction at positive pitch, zero pitch, and negative (reverse) pitch positions
     SearchKeywords: propeller reverse pitch negative blade angle airflow direction diagram -->

---

## Purpose of the 3D Demonstrator Model

This 3D demonstrator is not a working replica of a real C-130 propeller system. In the real aircraft, the hydraulic governor, propeller control unit, fuel control, torquemeter, reduction gearbox, NTS system, aerodynamic loads, and flight conditions all work together.

In the model, this complex system is represented by a servo motor, DC motor, potentiometer levers, amber LED, toggle switch, and software curves.

The model has three main visual objectives:

1. **Show blade angle changes** — Physically demonstrate how the servo-controlled blade angle responds to Power Lever movement.
2. **Show propeller speed representation** — Demonstrate how the DC motor PWM value changes or remains constant in different operating modes.
3. **Visualise the AIR START / unfeather process** — Show the unfeathering process step by step through amber LED and linear blade angle animation.

Therefore, the model is not a flight simulator; it is a turboprop propeller control demonstrator prepared for technical education and presentations.

<!-- VISUAL PLACEHOLDER: Photograph
     Description: Close-up photograph of the servo-controlled blade angle mechanism
     SearchKeywords: servo controlled variable pitch propeller mechanism model closeup -->

---

## Power Lever and Condition Lever Distinction

To understand the engine control logic in the C-130 family, the distinction between Power Lever and Condition Lever is essential. The C-130 flight manual states that four pedestal-mounted condition levers are the primary controls for engine starting/stopping and propeller feathering/unfeathering. These levers operate both mechanical linkages and switches that provide electrical control. The manual defines four placarded positions for the Condition Lever: RUN, AIR START, GROUND STOP, and FEATHER. ([Uniforce-SOG][4])

The **Power Lever** is the main lever that determines the pilot's power demand. In the Flight Range, engine power and the governor system work together; when the Power Lever is advanced, the system represents a greater power/torque demand and the governor changes blade angle to try to keep propeller RPM close to constant. In the Ground Range, blade angle becomes a direct function of throttle lever position and the propeller RPM governing logic does not work as it does in the flight range. ([Uniforce-SOG][4])

The **Condition Lever** should not be thought of as a direct "blade angle lever." In C-130/T56 logic, this lever manages the engine's operating state, fuel/ignition control, feather/unfeather signals, and the air-start process.

<!-- TABLE: Condition Lever Positions and Functions -->

| Position | Type | Function |
|---|---|---|
| **RUN** | Detent (locked) | Places engine fuel and ignition systems under speed-sensitive control. In this position, the Condition Lever has no direct control over the propeller. |
| **AIR START** | Held against spring force | Closes the same switch as RUN; additionally activates the propeller auxiliary pump switch to provide hydraulic pressure for unfeathering. |
| **GROUND STOP** | Detent (locked) | Closes the electrical fuel shutoff valve when the touchdown system is in ground mode. Also enables the nacelle preheat control circuit. |
| **FEATHER** | Mechanical linkage + switch | Transmits mechanical movement to the propeller and fuel control shutoff valve via the engine-mounted coordinator; sends mechanical and electrical feather signals to the propeller. |

*Source: C-130 Flight Manual, CGTO 1C-130-1 ([Uniforce-SOG][4])*

Demonstrator modes used for the Condition Lever in the model:

| Real Position | Model Mode | Demonstrator Behaviour |
|---|---|---|
| FEATHER | PROP FEATHER | Motor PWM = 0, blade angle → 93°, Power Lever ignored |
| GROUND STOP | PROP DEMO | Motor does not run, Power Lever changes only blade angle |
| RUN | NORMAL OPERATION | Two different PWM–blade angle curves depending on toggle switch |
| AIR START | UNFEATHER DEMO | LED animation + linear blade angle transition (93° → 23°) |

<!-- VISUAL PLACEHOLDER: Photograph
     Description: Power lever and condition lever placement on the pedestal in a C-130 cockpit
     SearchKeywords: C-130 cockpit throttle quadrant power lever condition lever pedestal -->

---

## GROUND STOP and GROUND IDLE Terminology Distinction

Terminology is particularly important at this point. In the real C-130E/H/T56 system, **GROUND STOP** is a position on the Condition Lever and is used to shut down the engine. In contrast, **GROUND IDLE** is associated with the ground operating position on the Power Lever / throttle side; it is the position in the beta range below Flight Idle where the propeller blades are at low positive pitch and the engine operates at minimum ground speed.

The flight manual calls for checking "throttles in ground idle" while moving the condition levers to GROUND STOP during engine shutdown. That is, Ground Idle and Ground Stop are not the same position on the same lever; they are different positions on different levers. ([Uniforce-SOG][4])

<!-- TABLE: GROUND STOP vs GROUND IDLE Comparison -->

| Term | Which Lever | Function | Position Type |
|---|---|---|---|
| **GROUND STOP** | Condition Lever | Engine shutdown (fuel cutoff) | Detent position |
| **GROUND IDLE** | Power Lever (Throttle) | Minimum ground operating power | Detent below Flight Idle |

Therefore, the model uses the designation **GROUND STOP / PROP DEMO**. Here, GROUND STOP corresponds to the real C-130 Condition Lever position. PROP DEMO is the model's additional educational behaviour; no such demonstration mode exists in the real aircraft.

---

## FEATHER / PROP FEATHER Mode

In FEATHER mode, the model represents the propeller being brought to the feathered position after an engine failure or engine shutdown.

In this mode, motor PWM is reduced to zero, blade angle goes to approximately 93° feather position, and the Power Lever is ignored. This allows the model to visually demonstrate the propeller being brought parallel to the airflow to reduce drag.

In the real C-130 Condition Lever description, when pulled to FEATHER, mechanical linkages transmit movement to the propeller and engine fuel control shutoff valve via the engine-mounted coordinator; mechanical and electrical feather signals are sent to the propeller. ([Uniforce-SOG][4])

<!-- VIDEO PLACEHOLDER: C-130 Engine Shutdown and Feathering
     Description: Real C-130 cockpit footage of the condition lever being pulled to FEATHER and propeller feathering
     Example URL: https://www.youtube.com/watch?v=5wKr6YmzTgM
     SearchKeywords: C-130 condition lever feather engine shutdown cockpit video -->

<!-- DIAGRAM PLACEHOLDER: Feather Position Schematic
     Description: Cross-section diagram showing blade angle (~90°+), airflow direction, and minimum drag condition in feather position
     SearchKeywords: propeller feather position blade angle cross section airflow diagram -->

---

## NTS: Negative Torque Sensing System

When discussing feather and air-start logic, it is necessary to address the NTS system. In the C-130/T56 system, NTS is a mechanical signal system used to limit negative torque conditions. Negative torque occurs when the propeller attempts to drive the engine — that is, when the propeller, instead of being driven by the engine, begins to drive the engine due to wind or other external factors. If this condition is not resolved, it creates significant drag and can cause the aircraft to yaw.

The flight manual explains that the NTS system works with mechanisms located in the reduction gear assembly and propeller valve housing, and that when negative torque exceeds a certain value, it affects the propeller valve housing linkages. ([Uniforce-SOG][4])

When the NTS signal is received, the system increases blade angle (toward coarser pitch) to relieve the condition. An important distinction here is: **normal NTS operation does not mean locking the propeller directly into full feather.** The manual states that normal NTS operation does not "commit" the propeller to feather, but that a malfunctioning NTS system could drive the propeller fully to feather or cause engine stall/flameout. ([Uniforce-SOG][4])

When the Power Lever is moved below Flight Idle, a cam mechanism moves the NTS actuator away from the NTS plunger and disables the system. This is to prevent the propeller from receiving unwanted negative torque signals, particularly when the throttle is moved toward the reverse side during high approach speeds. ([Uniforce-SOG][4])

NTS is not physically implemented in the model. However, the process indicated by the amber LED during AIR START can conceptually be linked to the fact that NTS is one of the critical indicators monitored during the air-start procedure in the real system. In the real C-130 air-start checklist, the flight engineer is asked to monitor NTS action and call "NTS" when the NTS check light illuminates. ([Uniforce-SOG][4])

<!-- DIAGRAM PLACEHOLDER: NTS System Schematic
     Description: Simplified schematic showing the NTS mechanism's position within the reduction gear, propeller valve housing, and blade angle feedback loop
     SearchKeywords: T56 Negative Torque Sensing NTS system reduction gear propeller schematic -->

---

## GROUND STOP / PROP DEMO Mode

The GROUND STOP / PROP DEMO mode is an intermediate mode used for safe demonstration in the model. In the real C-130/T56 system, GROUND STOP is the engine shutdown position on the Condition Lever. The manual calls for moving the condition levers to GROUND STOP and observing fuel flow dropping to zero during engine shutdown. ([Uniforce-SOG][4])

PROP DEMO behaviour has been added to this mode in the model. In this mode, the DC motor is not run. The Power Lever remains active and only blade angle is changed. This allows the observer to clearly see how the blades change angle without the propeller rotating.

This behaviour is not a direct counterpart of the real aircraft; it is a model behaviour added for educational and safe presentation purposes. It is particularly useful for mechanical testing, servo calibration, and explaining blade angle movement.

<!-- VISUAL PLACEHOLDER: Photograph / Short Video
     Description: Demonstration of blade angle change via servo without motor running in PROP DEMO mode
     SearchKeywords: propeller pitch change servo demonstration model static -->

---

## RUN Mode and Toggle Switch Logic

Two different operating approaches have been used for RUN mode in the model. A small toggle switch will be added to the panel for this purpose. This switch will only change the PWM–blade angle curve within RUN mode. The basic behaviour of FEATHER, GROUND STOP / PROP DEMO, and AIR START modes will not change.

The toggle switch will have two positions:

| Position | Mode Name | Behaviour |
|---|---|---|
| Position 1 | C-130 / Constant-Speed RUN | Motor PWM nearly constant, blade angle changes with Power Lever |
| Position 2 | General Turboprop Pitch/RPM Demo RUN | RPM and blade angle change inversely |

This allows the model to demonstrate both C-130/T56 constant-speed logic and general turboprop educational logic in a more understandable way.

<!-- VISUAL PLACEHOLDER: Photograph
     Description: Close-up view of the toggle switch on the panel with mode labels
     SearchKeywords: toggle switch panel mode selector labeled closeup -->

---

## RUN Mode 1: C-130 / Constant-Speed RUN

This mode has been designed to be closer to the constant-speed propeller logic in the C-130 family. In this approach, the engine/propeller speed is kept close to constant. As the Power Lever is advanced, the main visual change occurs on the blade angle side.

The logic is as follows:

1. The Power Lever is advanced.
2. The model represents a greater power/torque demand.
3. Blade angle increases.
4. Motor PWM value is kept close to constant rather than making large changes.

Representative blade angle transition in this mode: **0° → 5° → 23° → 35° → 55°**

This approach is suitable for explaining the governor logic in the C-130/T56 system. Because in the flight range, the propeller governor system tries to maintain constant RPM; blade angle, fuel flow, and torque change together. The C-130 flight manual explains that in the Flight Range, propeller speed is kept at constant RPM and that in an overspeed condition, the pilot valve increases blade angle to slow the propeller. ([Uniforce-SOG][4])

<!-- GRAPH PLACEHOLDER: Constant-Speed RUN — PWM and Blade Angle Curve
     Description: Dual-axis line graph showing motor PWM (nearly flat line) and blade angle (increasing curve) against Power Lever position
     Axes: X = Power Lever position (%) | Y₁ = Motor PWM (%) | Y₂ = Blade angle (°)
     SearchKeywords: constant speed propeller blade angle vs power lever graph PWM constant -->

---

## RUN Mode 2: General Turboprop Pitch/RPM Demo

The second RUN mode is not intended to represent the real C-130 behaviour one-to-one; rather, it is designed to make general turboprop and constant-speed propeller educational logic more understandable.

In this mode, when the lever is advanced, high RPM + low/fine pitch behaviour is shown. When the lever is pulled back, low RPM + high/coarse pitch behaviour is shown. This relationship is seen more directly in piston-engine constant-speed propeller systems where the pilot can select propeller RPM with a separate prop control lever, and in some turboprop training presentations. The FAA training material states that a low-pitch/high-RPM setting is used for takeoff, and a higher pitch with lower RPM setting can be used after takeoff. ([Federal Aviation Administration][7])

**However, this mode is not the real flight range behaviour of the C-130/T56 system.** In the C-130, during normal flight range operation, instead of "RPM continuously increases" when the Power Lever is advanced, the governor keeps RPM close to constant and power changes are effected primarily through torque, fuel flow, and blade angle. Therefore, this mode should be labelled on the model not as "C-130 real mode" but as **General Turboprop Pitch/RPM Demo** mode.

<!-- GRAPH PLACEHOLDER: General Turboprop Demo — RPM and Blade Angle Curve
     Description: Dual-axis line graph showing RPM increasing and blade angle decreasing (or vice versa) as Power Lever advances in this mode; side-by-side comparison with the Constant-Speed RUN graph
     Axes: X = Power Lever position (%) | Y₁ = Motor PWM/RPM (%) | Y₂ = Blade angle (°)
     SearchKeywords: turboprop RPM vs blade pitch general education diagram graph -->

---

## AIR START / UNFEATHER Demo Logic

The AIR START mode will visually represent the unfeathering and restart process in the model. In the real C-130/T56 system, AIR START is a position where the Condition Lever is held forward against spring force. The flight manual explains that the AIR START position closes the same switch as RUN, additionally activates the propeller auxiliary pump switch, and that this provides pressure to unfeather the propeller. When the auxiliary pump is operating, hydraulic fluid is routed to the aft side of the dome assembly piston to move the blades to a low-pitch angle. ([Uniforce-SOG][4])

In the real normal air-start checklist, there is a preparation process that assumes propeller rotation has stopped following engine shutdown. The checklist notes that the condition lever is initially assumed to be in the FEATHER position, the recommended air-start speed is 180 KIAS or below, and the Condition Lever is held in the AIR START position and released to RUN after light-off. ([Uniforce-SOG][4])

### Model AIR START Sequence

<!-- TABLE: AIR START Demo Step Sequence -->

| Step | Event | Blade Angle | Motor PWM | Amber LED |
|---|---|---|---|---|
| 1 | Start — propeller in feather, engine off | 93° (fixed) | 0 | Off |
| 2 | AIR START command detected | 93° (fixed) | 0 | Flashes 2× |
| 3 | Unfeather begins | 93° → 55° | 0 → low | Steady on |
| 4 | Unfeather continues | 55° → 35° | Low → medium-low | Steady on |
| 5 | Light-off representation / sequence end | 35° → 23° | Medium-low → medium | Steady on |
| 6 | AIR START complete | 23° (fixed) | Medium (fixed) | Off |
| 7 | User moves Condition Lever to RUN | 23° (starting) | Linked to Power Lever | Off |

In the real aircraft, the AIR START position is spring-loaded and is released to RUN after light-off. Since the potentiometer used in the model cannot physically return to RUN on its own, this operation will be performed manually by the user.

<!-- FLOWCHART PLACEHOLDER: AIR START Sequence Flow
     Description: Step-by-step flowchart of the AIR START demo process — initial condition, LED signal, unfeather transitions, motor PWM increase, and sequence completion decision
     SearchKeywords: turboprop air start restart sequence flowchart unfeather steps -->

<!-- VIDEO PLACEHOLDER: C-130 Air Start Procedure
     Description: Real or simulator environment footage of the C-130 air start procedure
     SearchKeywords: C-130 air start procedure cockpit video inflight restart -->

---

## Software and Electronics Enhancements

The basic structure of the Cadly turboprop model is sufficient for a simple propeller display. However, in this project, the model is being transformed into a more instructional demonstrator.

For this purpose, the following features are being added to the system:

- Condition Lever with FEATHER, GROUND STOP / PROP DEMO, RUN, and AIR START behaviours
- Power Lever controlling blade angle and motor PWM curves
- Toggle switch for selecting between two different RUN modes
- Amber LED for AIR START status indication
- Servo for blade angle control
- DC motor for propeller rotation
- Slow and linear unfeather animation during AIR START
- PWM–blade angle curves representing governor logic in RUN mode

<!-- BLOCK DIAGRAM PLACEHOLDER: System Wiring Schematic
     Description: Block diagram showing connections between Arduino/microcontroller (centre), potentiometer (Power Lever), potentiometer (Condition Lever), toggle switch, servo motor, DC motor (via H-bridge), amber LED, and power supply
     SearchKeywords: Arduino servo DC motor H-bridge potentiometer toggle switch LED wiring block diagram -->

---

## Technical Limitations of the Model

The servo angle used in this model is not the direct counterpart of the real propeller blade angle mechanism. Nor should the motor PWM value be seen as a direct counterpart of real propeller RPM.

In the real aircraft, propeller load depends on airflow, flight speed, engine torque, reduction gear system, governor behaviour, hydraulic control system, NTS mechanism, and cockpit control logic. Not all of these effects are directly measured in the model. Instead, visual and educational representation is created through software-defined curves.

Therefore, the model's goal is **conceptual accuracy, not operational accuracy**. That is, the aim is not to work like a real aircraft, but to show what happens in the real system in an understandable way.

---

## Conclusion

The C-130 family is a powerful example for understanding the turboprop engine–propeller relationship. The classic T56/54H60 system represents single-shaft turboprop, mechanical/hydraulic governor, Condition Lever, and NTS logic, while modern propellers like the R391 offer hydraulic constant-speed, reversible, and full-feathering capabilities in a more advanced configuration.

The Cadly turboprop 3D model used in this project is being transformed into a more technical demonstrator with software and electronics additions. With AIR START animation, two different RUN modes selectable via toggle switch, FEATHER and GROUND STOP / PROP DEMO modes, the model provides a more understandable structure for both R391 visual appearance and the turboprop propeller control logic in the C-130 family.

In conclusion, this demonstrator is not a direct replica of C-130J/R391 or T56/54H60 systems. Instead, it is an instructional model that visually explains the fundamental concepts in these systems and can be used in technical presentations.

---

## References

1. Rolls-Royce — T56 official page: single shaft, modular design turboprop structure; 14-stage axial compressor, 4-stage turbine, and two-stage reduction gearbox information. ([Rolls-Royce][1])

2. Rolls-Royce — AE2100 official page: AE2100D3 engine usage in C-130J and LM-100J platforms. ([Rolls-Royce][2])

3. Smithsonian National Air and Space Museum — Dowty R391 propeller hydraulic constant-speed, reversible, and full-feathering features; six composite blades and 4.115 m diameter. ([National Air and Space Museum][3])

4. C-130 Flight Manual, CGTO 1C-130-1 — Condition Lever positions, RUN/AIR START/GROUND STOP/FEATHER functions, propeller speed control system, low pitch stop, NTS system, and air-start checklist details. ([Uniforce-SOG][4])

5. Lockheed Martin Service News — T56 100% engine speed 13,820 RPM, 13.54:1 reduction ratio, and approximately 1,021 RPM propeller speed. ([Lockheed Martin][5])

6. UK CAA / EASA — R391 Type Certificate Data Sheet: variable-pitch, constant-speeding, feathering, and reversing type; beta control, hydraulic control, counterweights, C-130J/LM-100J usage, and 1,020.7 RPM values. ([CAA][6])

7. FAA Aviation Maintenance Technician Handbook, Chapter 7 — General constant-speed propeller training with low-pitch/high-RPM takeoff and higher-pitch/lower-RPM post-takeoff usage. ([Federal Aviation Administration][7])

8. AFMAN 11-2C-130H Vol. 3 — Current C-130H operational document for Condition Lever – GROUND STOP usage during engine shutdown. ([E-Publishing][8])

[1]: https://www.rolls-royce.com/products-and-services/defence/aerospace/transport-tanker-patrol-and-tactical/t56.aspx "T56 | Rolls-Royce"
[2]: https://www.rolls-royce.com/products-and-services/defence/aerospace/transport-tanker-patrol-and-tactical/ae-2100.aspx "AE 2100 | Rolls-Royce"
[3]: https://airandspace.si.edu/collection-objects/propeller-variable-pitch-6-blade-dowty-r391/nasm_A20070022000 "Propeller, Variable-Pitch, 6-blade, Dowty R391 | National Air and Space Museum"
[4]: https://uniforce-sog.org/wp-content/uploads/2024/07/USCG-Lockheed-C-130-Flight-Manual.pdf "1C-130-1"
[5]: https://www.lockheedmartin.com/content/dam/lockheed-martin/aero/documents/sustainment/csc/service-news/sn-mag-v11-v20/V16N1.pdf "V16N1.pdf"
[6]: https://www.caa.co.uk/Documents/Download/3940/77d2f18a-4292-443a-8980-607aade5d45a/1112 "R391 TCDS"
[7]: https://www.faa.gov/sites/faa.gov/files/09_amtp_ch7.pdf "Chapter 7 - Propellers"
[8]: https://static.e-publishing.af.mil/production/1/af_a3/publication/afman11-2c-130hv3/afman11-2c-130hv3.pdf "AFMAN11-2C-130HV3"
