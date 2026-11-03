# Control logic and limitations

[Back to README](../README.md)

## Decision priority

After the touch-sensor start and initial outward/turn maneuver, the program repeats the following priority-ordered logic:

```text
Read color sensor RGB threshold
   |-- Edge found? YES -> retract mechanism, reverse, turn/search
   |-- NO -> Ultrasonic distance below threshold?
           |-- YES -> drive toward opponent, activate auxiliary motor
           |-- NO  -> retract mechanism if deployed; drive forward
```

## Key source-level parameters

| Item | Archived code behavior |
|---|---|
| Opponent detection | `getUSDistance(sonarSensor) < 40` |
| Edge criterion | `r >= 38 && g >= 38 && b >= 25` |
| Startup | Touch-sensor press, outward drive, edge detection, reverse, encoder-controlled turn |
| Backup | Drive motors at `-100`, left encoder target `-550` |
| Boundary scan | Opposed drive commands `75` and `-75`, stop at encoder threshold `2000` or opponent detection |
| Opponent detected | Drive speeds `80,80` and auxiliary-motor command `100` |
| Free movement | Drive speeds `80,80`, auxiliary-motor command `0` |

These are source-code settings, **not independently verified physical angle, distance, force, or speed measurements**. The movement comments describe intended turns, but actual rotation depends on gearing, wheel diameter, friction, chassis load and sensor/motor calibration.

## Engineering limitations

- RGB threshold values can vary with light, sensor height and ring reflectance.
- Ultrasonic readings alone do not establish reliable opponent tracking or identification.
- The control scheme is reactive and does not map opponents or optimize collision trajectories.
- Motor commands and encoder waits may block indefinitely if expected feedback fails; no timeouts or fault-handling state machine are implemented.
- The team reports finishing **2nd among 20 teams** in the course competition. Official standings, individual bout scores, and independently recorded performance data were not supplied for this repository.
- The medium motor retraction behavior is based on a fixed target; load and mechanism performance are not quantified.
- The uploaded program header labels the experiment **Lab 1**, whereas the supplied assignment document is titled **Project — SUMO**, and the source filename includes **Lab2**. Without an additional authoritative record, the repository describes it generically as an MSE 110 group project instead of assigning a definitive lab number.

## Source fidelity

The included `src/SumoRobot.c` preserves the historical logic and ROBOTC configuration while removing the three students' identification numbers and replacing the personal-information header. No functional code edits were made. Its compile and hardware behavior have not been reverified.
