# Autonomous Sumo Robot — LEGO Mindstorms EV3

**ROBOTC · LEGO EV3 · Ultrasonic sensing · RGB boundary detection · Motor encoders · Autonomous control**

An autonomous LEGO Mindstorms EV3 sumo robot developed as a **Group 17 project for MSE 110: Mechatronic Design I at Simon Fraser University**. The team **placed second out of 20 teams** in the course sumo competition. Its ROBOTC program combines opponent detection, arena-boundary avoidance, and a motorized auxiliary-wheel mechanism for contact with opposing robots.

<p align="center"><img src="media/Sumo%20Robot.jpg" alt="LEGO EV3 sumo robot prototype with front ultrasonic sensor and mechanical extension" width="720" /></p>

## Project overview

The course challenge involved two autonomous robots attempting to push or disable one another within a circular black arena with a white perimeter. The assignment specified an initial outward movement followed by an encoder-based turn before engagement. The source implements that startup sequence and then runs a reactive, priority-ordered control loop.

| Category | Implementation |
|---|---|
| Platform | LEGO Mindstorms EV3 |
| Language | ROBOTC, EV3-specific motor and sensor functions |
| Drive | Two EV3 large motors, left on port A and right on port D |
| Mechanism | EV3 medium motor on port B for an auxiliary wheel / arm |
| Sensors | Touch sensor (S1), ultrasonic sensor (S2), color sensor in RGB mode (S3) |
| Strategy | Start sequence; boundary avoidance takes priority; charge detected opponent; otherwise search/advance |
| Artifacts | Privacy-reviewed source, project photography, demonstration GIF, design notes |

## Autonomous control strategy

1. **Start:** Wait for a press on the touch sensor.
2. **Initial positioning:** Drive outward until the RGB threshold indicates the white border; reverse, then make an encoder-controlled turn intended to face into the arena.
3. **Boundary avoidance (highest priority):** When the color sensor detects the border, reverse and rotate to search for the opponent.
4. **Opponent engagement:** If ultrasonic distance is below the configured **40-unit threshold** (the ROBOTC distance call is normally expressed in centimetres), advance with both drive motors while powering the auxiliary mechanism.
5. **Search / advance:** When no edge or opponent is detected, continue forward and retract the auxiliary mechanism if previously deployed.

This is **reactive rule-based control**, not autonomous mapping, target tracking, or a formal optimal-strategy planner. The source uses fixed sensor thresholds and encoder targets, which would require recalibration for different surfaces and chassis configurations.

For sensor configuration, state transitions, and firmware details, see [System Design](docs/SYSTEM_DESIGN.md) and [Control Logic and Limitations](docs/CONTROL_AND_LIMITATIONS.md).

## Robot photographs and demonstration

<p align="center"><img src="media/Maximizing%20torque%20against%20bigger%20opponent.jpg" alt="LEGO EV3 sumo robot engaged with a larger opposing robot in the arena" width="720" /></p>

*Physical robot engagement with a larger opponent; the available media does not establish an official match result.*

<p align="center"><img src="media/Sumo%20In%20Action.gif" alt="Animated EV3 sumo robot demonstration in the competition ring" width="720" /></p>

*Sumo competition demonstration showing the robots operating in the arena.*

## Source code

- [ROBOTC program](src/SumoRobot.c) — archived control logic with student identifiers removed.
- [System Design](docs/SYSTEM_DESIGN.md) — hardware, sensor inputs, and actuation architecture.
- [Control Logic and Limitations](docs/CONTROL_AND_LIMITATIONS.md) — startup sequence, decision priority, assumptions, and reproducibility limitations.

Open the C file in a version of **ROBOTC compatible with EV3** and confirm the configured motor/sensor ports before deploying to hardware. The source has not been independently compiled or retested for this publication.

## Results and engineering limitations

**Competition result:** Group 17 finished **2nd place among 20 participating teams**, as reported by a team member. The photographs document the physical EV3 robot and an arena encounter, while the code documents its autonomous control strategy. Individual bout scores, pushing-force measurements, sensor calibration logs, and reproducible timing benchmarks were not provided; therefore, no specific match victories or quantitative performance figures are claimed.

The original code also includes blocking encoder and sensor loops without explicit timeouts. These can stall if expected motor or sensor feedback does not arrive. See [Control Logic and Limitations](docs/CONTROL_AND_LIMITATIONS.md).

## Collaboration and attribution

This is an **academic group project (MSE 110, Group 17)**; project outcomes should not be interpreted as solely individual work. The original source included student ID numbers, which have been removed from the public copy. The university's assignment description was used for background but is **not included** in this repository. No license is granted merely by making the files public.

## Portfolio

**Hasan Fairuz** — Mechatronic Systems Engineering

[Engineering Portfolio](https://hasanfairuz.com/) · [GitHub Profile](https://github.com/HasanFairuz)
