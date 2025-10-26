# Demonstrations for Delay-Kirk with Teams of Drones

## Hardware Demonstration Scenario

- Two teams A and B, each with 2 drones.
- Each destination is a communication hotspot i.e starts and ends of each drones are the only places where they can communicate with the command server or other teams.
- Communication with the command serve is reliable but unreliable with other teams
- Everywhere else is a dead-zone.
- A starts first and finishes its mission.
- A then uploads its data to the command server.
- Now here delay comes into play. Since A and B cannot talk directly to each other, the command server has to bridge that gap which introduces the delay.
- B starts **after** A finishes uploading its data to the command server. 
- B repeats the same process as A until it finishes and uploads it data to the command server.
- Each demo will be supplemented by a simulation-only video in visual and non-visual environments as backup.
- Current setup is scalable to more teams and more drones within teams and more missions as well.

Mission A: Time Bound - [lb_A, ub_A], Delay Bound - [dl_A, du_A]

Upload A: Time Bound - [upl_A, upu_A]

Mission B: Time Bound - [lb_B, ub_B], Delay Bound - [dl_B, du_B]

Upload B: Time Bound - [upl_B, upu_B]

- Missions are contingent events i.e they need to be acknowledged.
- Let $d_A \in [dl_A, du_A]$ be the delay after $t_A$ when team B receives the unreliable acknowledgement of team A.
- Let $t_A^B = min(ub_A, t_A + d_A)$ be the time when B receives the unreliable acknowledgement of team A.
- "xxxxxxx" denotes minimum bound of the communication delay i.e dl_A in this context. 

```
Timelines:   t=0|---------------------------------------------------------------------------------------------------|t=$\infty$ 

A's perspective:                                    
                  $lb_A$        $t_A$                $ub_A$
Mission A:         |--------------|--------------------|
                                  |      $t_A+upl_A$   |                        $t_A+upu_A$
Upload A:                         |          |--------------------------------------|
                                  |          
                                  |          
B's perspective:                  |              
                                  | $t_A+dl_A$           $t_A+du_A$                             
Mission A:                        |xxxxx|----Case 1-----|---Case 2------|
                                  |    
Upload A:                         |xxxxx|--|--------------------------------------| 
                                    $t_A^B + max(0, upl_A-dl_A)$           $t_A^B + max(0, upu_A-dl_A)$
Mission B:                                 |-----------------------------|---------------------|
                                     $t_A^B + max(0, upl_A-dl_A) + lb_B$ |    $t_A^B + max(0, upl_A-dl_A) + ub_B$
Upload B:                                                                |-------------------------|
                                                                    $t_B + upl_B$             $t_B + upu_B$
```

## Objectives of the demos:
- First Demo: Behavior of Kirk/Delay-Kirk will be similar.
- Second Demo: Delay-Kirk will not crash in scenarios where the communication delay exceeds the mission duration bounds
- Third Demo: Delay-Kirk will be able to finish the overall mission faster due to its ability to compensate for communication delays

## Delay Kirk

- First Demo:
  - No delay, Expected behavior: A starts and finishes, A communicates that it has finished and then B starts its mission and finishes
  - [x] Sim
  - [ ] Hardware
- Second Demo:
  - Non-zero delay,
  - Cases are defined based on when B receives information about A's acknowledgement. Lets assume A finishes at $t_A \in [lb_A, ub_A]
    - Case 1:  B receives A's ack within t_A^B \in [t_A + dl_A, ub_A]
      - Expected Behavior: B will start its mission at t_A^B
      - [x] Sim
      - [ ] Hardware
    - Case 2:  B receives A's ack within t_A^B \in [ub_A, t_A + du_A]
      - Expected Behavior: B will start its mission at ub_A + upl_A
      - [ ] Sim
      - [ ] Hardware
- Third Demo:
  - Non-zero large delays,
  - Follow case 1 from previous demo,
  - Expected behavior: Will finish the overall mission faster
  - [x] Sim
  - [ ] Hardware

## Kirk

- First Demo:
  - No delay, Expected behavior: Same
  - [ ] Sim
  - [ ] Hardware
- Second Demo:
  - Non-zero delay,
  - Cases are defined based on when B receives information about A's acknowledgement. Lets assume A finishes at $t_A \in [lb_A, ub_A]
    - Case 1:  B receives A's ack within t_A^B \in [t_A + dl_A, ub_A]
      - Expected Behavior: mission will finish later than delay-kirk
      - [ ] Sim
      - [ ] Hardware
    - Case 2:  B receives A's ack within t_A^B \in [ub_A, t_A + du_A]
      - Expected Behavior: planner will crash leading to failure of the overall mission
      - [ ] Sim
      - [ ] Hardware
- Third Demo:
  - Non-zero large delays,
  - Follow case 1 from previous demo,
  - Expected behavior: Mission will finish much later than the corresponding delay-kirk demonstration
  - [ ] Sim
  - [ ] Hardware
