rclcpp_wake_latency
====

## About
Check ROS 2 rclcpp wake latency.

## Environment
- Ubuntu 18.04
- ROS 2 Eloquent
- FastRTPS
  - I didn't check other DDS.

## Build

```
# git clone
colcon build --symlink-install
```

## Run
Do following, and stop by C-c.

```
./build/wake_latency/main_cyclic_node
```

After run `cyclic_component.txt` is created.
4th column means jitter between real and expected wake up time.
Unit is [ns].

```
$ head cyclic_component.txt
now, expect, last_fin, now-expect, now-last_fin
8494268887615476, 8494268887368630, 8494268877368700, 246846, 10246776
8494268897573480, 8494268897368630, 8494268887641033, 204850, 9932447
8494268907573710, 8494268907368630, 8494268897597264, 205080, 9976446
8494268917576971, 8494268917368630, 8494268907597558, 208341, 9979413
8494268927564609, 8494268927368630, 8494268917600798, 195979, 9963811
8494268937577161, 8494268937368630, 8494268927584935, 208531, 9992226
8494268947577787, 8494268947368630, 8494268937600928, 209157, 9976859
8494268957583062, 8494268957368630, 8494268947601818, 214432, 9981244
8494268967576718, 8494268967368630, 8494268957606779, 208088, 9969939
```

In my environment, this increased linearly...
- Axis
  - vertical: jitter in nano-second
  - horizontal: number of iterations
- Lines
  - Blue: wake timer jitter i.e. wake up time - expected time (column 4 above)
  - Orange: difference between wake up time - last wake up time (column 5 above)

![jitters](https://user-images.githubusercontent.com/60122040/76944087-c2ca8900-6943-11ea-98fe-8b56401afc9a.png)
