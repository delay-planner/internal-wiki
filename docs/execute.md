# Execute Code on Highbay

This is a series of commands used on the highbay machines.

## Run

```
ros2 launch rbmapf_gzsim integrated_sim_demo.launch.py num_drones:=4 backend:=sim use_hardware:=False
```

Edit the rmpl passed in

--------------------------------------

## Archive

### Multi-drone, multi-mission distributed Kirk

1. Launch the main crazyswarm launch.py with cflib

```
ros2 launch crazyflie launch.py backend:=cflib
```

2. Start the middleware server

```
cd /home/mers/Developer/kirk_setup
source venv/bin/activate
python3 distr.py
```

3. Run the crazyflies, wait till they're hovering

```
bash execute.sh
```

4. Run Kirk

```
podman start 3d2642905d0e
podman exec -it 3d2642905d0e /bin/bash
bash execute_kirk.sh
```

### Run the Multi-Drone Planner

```
podman start 3d2642905d0e
podman exec -it 3d2642905d0e /bin/bash
kirk run kirk-v2/examples/drone-case/easy.lisp -P scenario1     --driver-command 'curl -X POST -H "Content-Type: application/json" -d "{\"data1\":\"~A\", \"data2\":\"~A\"}" http://localhost:5000/submit' --tolerance 0.5 -p 8000 --verbose &
```

```
cd /home/mers/Developer/kirk_setup
source venv/bin/activate
python3 main.py
```

```
ros2 launch crazyflie_examples launch.py script:=hello_world backend:=cflib
```
