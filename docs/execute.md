# Run the Multi-Drone Planner

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
