# System design

[Back to README](../README.md)

## Platform and electrical configuration

The archived ROBOTC configuration identifies a LEGO Mindstorms EV3 controller with three motors and three input sensors.

| EV3 port | Assigned component | Role |
|---|---|---|
| Motor A | Left large motor | Left drive wheel |
| Motor B | Medium motor (`armMotor`) | Mechanism described in source as retracting a third wheel |
| Motor D | Right large motor | Right drive wheel |
| Sensor 1 | Touch sensor | Starts the autonomous routine |
| Sensor 2 | Ultrasonic sensor | Detects an approaching opponent |
| Sensor 3 | Color sensor, RGB mode | Detects the high-reflectance perimeter |

## Physical arrangement

The supplied photographs show a compact EV3 sumo assembly with exposed Technic structural members, wide drive tires, a forward-mounted ultrasonic module and a front auxiliary mechanism. The second image shows the prototype near a larger opponent in the arena. Exact chassis geometry, gear ratios, and pushing force are not documented.

![Robot prototype](../media/Sumo%20Robot.jpg)

## Assignment context (not redistributed)

The course brief specified a circular ring about 122 cm in diameter with a white perimeter about 5 cm wide. It also required an initial outward approach to the edge followed by an encoder-based turn before looking for the opponent. This reference establishes **competition constraints**, not independently measured system performance.

## Reproducibility

The hardware mapping comes from the uploaded source and is not independently verified against an assembled EV3 device. Reproducing the project requires compatible LEGO EV3 hardware, the ROBOTC toolchain, suitable arena materials and sensor/encoder calibration.
