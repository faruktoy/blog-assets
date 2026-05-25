---
title: "Propeller Control Logic in Turboprop Engines: A C-130-Inspired 3D Training Model"
date: "May 21, 2026"
readTime: "10 min read"
tags: "Turboprop, C-130, T56, R391, 3D Printing, Propeller Control"
---

# Propeller Control Logic in Turboprop Engines: A C-130-Inspired 3D Training Model

> From the outside, turboprop engines may look simple: the engine turns, the propeller pushes air, and the aircraft moves forward. In large turboprop aircraft, however, the system is not simply about “spinning a propeller.” How engine power is transferred to the propeller, how propeller RPM is controlled, how blade angle changes, and how the governor balances these variables must all be considered together.
>
> This project was created to make that logic visible. The model I built is not a working replica of a real aircraft system; it is an educational demonstrator designed to make the turboprop engine-propeller relationship easier to understand. The external geometry is inspired by the modern six-blade R391-style propeller, while the control logic is based on the T56, constant-speed, and condition lever principles seen in the C-130 family.

<!-- VISUAL PLACEHOLDER: Hero / Poster
     Description: Main poster or cover image for the C-130-inspired turboprop training model
     SearchKeywords: C-130 turboprop training model T56 R391 propeller control infographic -->

## How Is Power Transferred to the Propeller in a Turboprop Engine?

A turboprop engine is a system in which a gas turbine engine works together with a propeller. Air is compressed inside the engine, mixed with fuel, and burned; the high-energy gas then produces power through the turbine. Roughly 80-90% of the turbine output is transferred to the propeller through a reduction gearbox, while the remaining 10-20% contributes to residual jet thrust.

The reduction gearbox is a critical part of this system. While the turbine side operates at very high speeds, often in the range of 11,000-14,000 RPM, the propeller must rotate at a lower speed with higher torque. Rolls-Royce describes the T56 as a single-shaft, modular-design turboprop engine with a 14-stage axial compressor, a 4-stage turbine, and a two-stage reduction gearbox.

In large turboprop aircraft such as the C-130, this power transfer is not just a mechanical connection. The blade angle, or how much the propeller “bites” the air, also determines how much power the propeller absorbs. For that reason, the propeller is not a passive rotating part; it is an actively controlled system that transfers engine power into the air.

![Turboprop Power Transfer Diagram](https://cdn.jsdelivr.net/gh/faruktoy/blog-assets@blog/image/TurboProp/turboprop-power-transfer.png)
<!-- DIAGRAM PLACEHOLDER: Turboprop Power Transfer Diagram
     Description: Simple schematic showing power transfer between the air inlet, compressor, combustion chamber, turbine, reduction gearbox, and propeller
     SearchKeywords: turboprop engine power flow reduction gearbox propeller diagram -->

![Power Distribution](https://cdn.jsdelivr.net/gh/faruktoy/blog-assets@blog/image/TurboProp/turboprop-power-thrust-vs-speed.png)
<!-- PLOT PLACEHOLDER: Power Distribution
     Description: Bar or donut chart showing that most turbine output goes to propeller shaft power, while a smaller portion remains as residual jet thrust
     Axes: Category = Propeller shaft power / Residual jet thrust | Value = Approximate ratio (%)
     SearchKeywords: turboprop power distribution propeller shaft residual thrust chart -->

## What Is a Variable-Pitch Propeller?

In a fixed-pitch propeller, the blade angle does not change, and the optimum angle of attack is generally around 2 to 4 degrees. This is a simple and durable solution, but it is not always efficient for every flight phase. Takeoff, climb, cruise, landing, and engine failure all require different propeller behaviour.

In a variable-pitch propeller, the blades can rotate around their own axes and move to different angles of attack. At low blade angle, the propeller loads the air less and turns more easily. At high blade angle, the propeller interacts with more air on each rotation and creates a higher aerodynamic load.

This idea can be compared to gear ratios in a car. Low blade angle is like a low gear: the engine can accelerate more easily. High blade angle is like a higher gear: the system carries more load but works more efficiently at the right speed.

<!-- DIAGRAM PLACEHOLDER: Blade Angle and Feather View
     Description: Technical diagram explaining low pitch, high pitch, and full feather positions using side-view and/or cutaway-style propeller views
     SearchKeywords: variable pitch propeller low pitch high pitch feather diagram -->

<!-- TABLE: Representative Blade Angle Values Used in the Model -->

| Operating Region | Representative Blade Angle | Description |
|---|---:|---|
| Low Pitch / Ground | ~0° – 5° | Propeller at minimum aerodynamic load |
| Flight Idle / Low Pitch Stop | ~23° | Minimum flight angle allowed by the governor |
| Takeoff / Climb | ~23° – 35° | High power, increasing blade angle |
| Cruise / High Pitch | ~35° – 55° | High blade angle for cruise efficiency |
| Full Feather | ~93° | Blade nearly parallel to airflow; minimum drag |

## Constant-Speed Logic

One of the most important concepts in this article is constant-speed propeller logic. In a constant-speed system, the goal is to keep propeller RPM close to a target value. When the pilot or the system requests more power, the engine produces more torque. The propeller tends to accelerate; the governor responds by changing blade angle so that the propeller absorbs more load. This allows power to increase while propeller RPM remains nearly constant.

FAA training material explains that a low-pitch / high-RPM setting can be used for takeoff, while a higher-pitch / lower-RPM setting can be used later in flight for efficiency. However, in systems such as the C-130/T56, this relationship should not be read directly as “lever forward = RPM increases.” C-130 flight documentation explains that in the flight range, propeller speed is held at constant RPM by the governor system, while in the ground range blade angle is more directly linked to throttle / power lever position.

For this reason, it made more sense to use two different RUN logics in the model. The first mode is closer to C-130 constant-speed behaviour: as the Power Lever is advanced, engine speed remains mostly near constant and the main visible change is blade angle. The second mode represents a more general turboprop training logic, showing the relationship between “high RPM + low pitch” and “low RPM + high pitch” in a more intuitive way.

<!-- DIAGRAM PLACEHOLDER: Governor Operating Principle
     Description: Schematic diagram showing the constant-speed propeller governor's pilot valve, flyweight, and blade angle feedback loop
     SearchKeywords: constant speed propeller governor pilot valve flyweight schematic -->

<!-- PLOT PLACEHOLDER: RPM vs Power Lever Position
     Description: Line graph showing that RPM remains nearly constant in a constant-speed system as the Power Lever advances, while blade angle and torque increase
     Axes: X = Power Lever position (%) | Y₁ = Propeller RPM | Y₂ = Blade angle (°) | Y₃ = Torque (ft-lbs)
     SearchKeywords: constant speed propeller RPM torque blade angle vs power lever graph -->

## Why Use the C-130 and T56 as an Example?

The C-130 family is a strong example for understanding the turboprop engine-propeller relationship. Classic C-130E/H models use the Allison, now Rolls-Royce, T56 engine and the 54H60 propeller system. On the more modern C-130J side, the aircraft uses the Rolls-Royce AE2100D3 engine and the Dowty/GE Aerospace R391 six-blade composite propeller system.

This project does not copy the real C-130J cockpit system one-to-one. The R391 appearance was chosen because it looks more modern and visually strong. The control logic, however, is aimed especially at explaining the condition lever, feather, ground stop, air start, and constant-speed concepts found in the T56/54H60 system.

Looking at different engine and propeller systems in the C-130 family reveals an interesting common point: propeller speed is controlled around roughly 1020 RPM. In the classic T56 system, the engine’s high rotational speed is reduced by the gearbox to around 1021 RPM at the propeller. In the R391 propeller used on the C-130J, the takeoff propeller speed is also given as approximately 1020.7 RPM. These values help explain why, in turboprop systems, propeller speed does not continuously increase as the Power Lever is advanced. In constant-speed logic, the system tries to keep propeller RPM nearly constant; what changes more directly is torque, fuel flow, and blade angle.

<!-- TABLE PLACEHOLDER: C-130 Propulsion Comparison
     Description: Comparison table for C-130E/H and C-130J focusing on engine, propeller, blade count, control character, and approximate propeller RPM
     Columns: System | Engine | Propeller | Blade Count | Main Control Character | Approx. Propeller RPM
     SearchKeywords: C-130E H T56 54H60 C-130J AE2100 R391 propeller comparison -->

<!-- VISUAL PLACEHOLDER: T56 / 54H60 and R391 Reference Image
     Description: Clean comparison visual showing the legacy T56/54H60 system and the modern R391-inspired six-blade appearance
     SearchKeywords: C-130 T56 54H60 propeller R391 six blade propeller comparison -->

## 3D Training Demonstrator Model

The aim of this model is not to copy a real C-130 propeller system one-to-one. In the real aircraft, the hydraulic governor, propeller control unit, fuel control, torquemeter, reduction gearbox, NTS system, and flight-condition-dependent aerodynamic loads all work together.

In the model, this complex real system is represented by a servo motor, a DC motor, potentiometer-based levers, a toggle switch, an amber LED, and software curves. The base 3D geometry uses Cadly’s Turboprop model; I would like to thank Cadly for the model geometry. Apart from that geometry, the electronic connections, control logic, lever modes, AIR START animation, and software side were developed specifically for this project.

The model has two main controls:

**Power Lever:** Represents the power demand. In RUN mode, depending on the selected operating approach, it affects the motor PWM value and blade angle curves.

**Condition Lever:** Represents the engine operating state. The model behaviour changes through the FEATHER, GROUND STOP, RUN, and AIR START positions.

In addition, the toggle switch is used to select between two different RUN logics. This allows the model to demonstrate both C-130 constant-speed behaviour and general turboprop pitch/RPM training logic.

<!-- VISUAL PLACEHOLDER: Photograph
     Description: General view of the 3D-printed turboprop demonstrator model
     SearchKeywords: 3D printed turboprop propeller pitch demonstrator model -->

<!-- VISUAL PLACEHOLDER: Control Panel Photograph
     Description: Close-up of the Power Lever, Condition Lever, toggle switch, amber LED, and electronic connections
     SearchKeywords: model aircraft power lever condition lever toggle switch LED Arduino servo DC motor -->

<!-- DIAGRAM PLACEHOLDER: Electronics Control Block Diagram
     Description: Block diagram showing the connections between the Power Lever, Condition Lever, toggle switch, controller board, servo motor, DC motor driver, and amber LED
     SearchKeywords: Arduino servo DC motor potentiometer lever toggle switch LED block diagram -->

## Operating Modes in the Model

The model uses four basic Condition Lever behaviours.

<!-- TABLE: Condition Lever Positions and Functions -->

| Position | Type | Function |
|---|---|---|
| **RUN** | Detent (locked) | Places the engine fuel and ignition systems under speed-sensitive control. In this position, the Condition Lever has no direct control over the propeller. |
| **AIR START** | Held against spring force | Closes the same switch as RUN; additionally operates the propeller auxiliary pump to provide hydraulic pressure for unfeathering. |
| **GROUND STOP** | Detent (locked) | Closes the electrical fuel shutoff valve when the touchdown system is in ground mode. It also provides nacelle preheat circuit control. |
| **FEATHER** | Mechanical linkage + switch | Transmits mechanical movement through the engine-mounted coordinator to the propeller and fuel control shutoff valve; sends mechanical and electrical feather signals to the propeller. |

*Source: C-130 Flight Manual, CGTO 1C-130-1 ([Uniforce-SOG][5])*

Demonstrator modes used for the Condition Lever in the model:

| Real Position | Model Mode | Demonstrator Behaviour |
|---|---|---|
| FEATHER | PROP FEATHER | Motor PWM = 0, blade angle → 93°, Power Lever ignored |
| GROUND STOP | PROP DEMO | Motor does not run; only blade angle changes with the Power Lever |
| RUN | NORMAL OPERATION | Two different PWM–blade angle curves depending on the toggle switch |
| AIR START | UNFEATHER DEMO | LED animation + linear blade angle transition (93° → 23°) |

<!-- DIAGRAM PLACEHOLDER: Condition Lever Positions
     Description: Single Condition Lever slot/arc diagram showing FEATHER, GROUND STOP, RUN, and AIR START positions
     SearchKeywords: C-130 condition lever FEATHER GROUND STOP RUN AIR START diagram -->

<!-- VIDEO PLACEHOLDER: C-130 Engine Shutdown and Feather
     Description: Real C-130 cockpit footage showing the Condition Lever being moved to FEATHER and the propeller feathering
     Example URL: https://www.youtube.com/watch?v=5wKr6YmzTgM
     SearchKeywords: C-130 condition lever feather engine shutdown cockpit video -->

**FEATHER / PROP FEATHER:**  
Motor PWM is reduced to zero, blade angle moves to approximately 93° feather position, and the Power Lever is ignored. This position demonstrates the logic of reducing drag after engine failure or engine shutdown.

**GROUND STOP / PROP DEMO:**  
In the real C-130 system, GROUND STOP is the engine shutdown position on the Condition Lever. In the model, an additional educational behaviour is assigned to this position: the motor does not rotate, but the Power Lever can still show blade angle movement. This is useful for mechanical testing and safe presentation.

**RUN / NORMAL OPERATION:**  
This is the normal operating mode of the model. Depending on the toggle switch position, two different RUN logics can be selected. In the C-130 constant-speed mode, engine speed remains near constant while blade angle increases. In the general turboprop demo mode, the RPM and pitch relationship is shown in a more training-oriented way.

**AIR START / UNFEATHER DEMO:**  
This mode visually represents the unfeathering and restart process. In the real C-130/T56 system, the AIR START position closes the same switch as RUN and also activates the propeller auxiliary pump circuit, providing hydraulic pressure for unfeathering. In the model, this process is represented by the amber LED indicator, slow blade angle transition, and motor PWM increase.

<!-- DIAGRAM PLACEHOLDER: AIR START / UNFEATHER Flow
     Description: Flow diagram showing the linear unfeather transition from 93° feather toward 23° low pitch, amber LED status, and manual RUN transition
     SearchKeywords: turboprop air start unfeather sequence feather to low pitch LED -->

<!-- PLOT PLACEHOLDER: Blade Angle and PWM During AIR START
     Description: Time plot showing blade angle decreasing from 93° to 23° while motor PWM gradually increases during the AIR START sequence
     Axes: X = Time (s) | Y₁ = Blade angle (°) | Y₂ = Motor PWM
     SearchKeywords: air start unfeather blade angle motor PWM time graph -->

## In Brief: What Is NTS?

NTS, or **Negative Torque Sensing**, is a protection logic in T56-powered C-130 systems that detects negative torque. Normally, the engine drives the propeller; however, in some failure or power-loss situations this relationship can reverse, and the propeller may begin to drive the engine due to airflow. This is called negative torque.

When negative torque occurs, the propeller can create serious drag and negatively affect aircraft control. The NTS system produces a signal to increase propeller blade angle. This moves the propeller toward a coarser pitch and reduces its tendency to drive the engine.

NTS is not physically implemented in this model. In other words, there is no real torque sensing or automatic protection mechanism in the system. Still, it is useful to mention NTS briefly, because it shows that turboprop propeller control is not just a matter of “the engine turns and the propeller turns.” In the real system, propeller behaviour, engine power, airflow, blade angle, and safety mechanisms work together.

<!-- DIAGRAM PLACEHOLDER: NTS Concept Diagram
     Description: Simple diagram showing the propeller attempting to drive the engine during negative torque and the NTS signal increasing blade angle to reduce drag
     SearchKeywords: Negative Torque Sensing T56 C-130 NTS propeller drag blade angle diagram -->

## Technical Limitations

This model is a conceptual demonstrator, so some limitations have been intentionally accepted.

First, the servo angle is not a direct equivalent of the real propeller blade angle mechanism. Second, the DC motor is controlled through PWM, and this value should not be treated as a direct equivalent of real propeller RPM. Third, the model does not include a real hydraulic governor, real torque feedback, real aerodynamic loading, or an NTS mechanism.

Also, because the current mechanical design does not support the negative blade angle region, reverse thrust has not been physically implemented. Although the software logic is aware of reverse behaviour, the current model focuses on low pitch, flight idle, cruise/high pitch, feather, and air-start/unfeather behaviour.

These limitations are not weaknesses of the model; they are a result of its purpose. The goal is not operational accuracy, but making turboprop propeller control logic understandable and visual.

<!-- TABLE PLACEHOLDER: Model Limitations
     Description: Table comparing which real-system functions are represented in the model and which are not physically implemented
     Columns: Feature | Represented in Model? | Real System Equivalent | Note
     SearchKeywords: 3D demonstrator model limitations turboprop propeller governor NTS reverse thrust -->

## Conclusion

In turboprop engines, the propeller is not merely a rotating part; it is an actively controlled system that transfers engine power into the air through blade angle and RPM control. The C-130 family provides a strong example for understanding this logic. The T56 engine, 54H60 propeller system, modern R391 propeller geometry, constant-speed logic, Condition Lever positions, and feather / air start processes form a useful technical foundation for this educational model.

The 3D demonstrator was designed to make this complex structure easier to understand. With servo-controlled blade angle, propeller rotation represented by a DC motor, Power Lever, Condition Lever, two RUN modes selected by a toggle switch, and AIR START animation, the model can visually explain the turboprop engine-propeller relationship.

This project is not a flight simulator or a copy of the real C-130 system. A more accurate definition would be: a 3D-printed educational model that explains power transfer, constant-speed propeller logic, and propeller control modes in turboprop engines.

<!-- VISUAL PLACEHOLDER: Final Poster / Summary Graphic
     Description: Final A3 poster or summary image showing the aircraft, T56/R391 concept, demonstrator model, Condition Lever, Power Lever, and project URL
     SearchKeywords: C-130 motor modeli turboprop demonstrator poster T56 R391 condition lever power lever -->

## References

[1]: https://www.rolls-royce.com/products-and-services/defence/aerospace/transport-tanker-patrol-and-tactical/t56.aspx "Rolls-Royce — T56 turboprop engine"
[2]: https://www.rolls-royce.com/products-and-services/defence/aerospace/transport-tanker-patrol-and-tactical/ae-2100.aspx "Rolls-Royce — AE2100 turboprop engine"
[3]: https://airandspace.si.edu/collection-objects/propeller-variable-pitch-6-blade-dowty-r391/nasm_A20070022000 "Smithsonian National Air and Space Museum — Dowty R391 propeller"
[4]: https://www.caa.co.uk/Documents/Download/3940/77d2f18a-4292-443a-8980-607aade5d45a/1112 "UK CAA / EASA — R391 Type Certificate Data Sheet"
[5]: https://uniforce-sog.org/wp-content/uploads/2024/07/USCG-Lockheed-C-130-Flight-Manual.pdf "C-130 Flight Manual, CGTO 1C-130-1"
[6]: https://www.lockheedmartin.com/content/dam/lockheed-martin/aero/documents/sustainment/csc/service-news/sn-mag-v11-v20/V16N1.pdf "Lockheed Martin Service News — T56 reduction ratio and propeller RPM"
[7]: https://www.faa.gov/sites/faa.gov/files/09_amtp_ch7.pdf "FAA Aviation Maintenance Technician Handbook — Chapter 7, Propellers"
