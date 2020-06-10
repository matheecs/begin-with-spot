# Spot 机器人介绍

[Boston Dynamics](https://www.bostondynamics.com)

* Marc Raibert
* Zachary Jackowski
* Russell Tedrake

## Spot 设计理念

![](.gitbook/assets/spotmini.jpg)

![&#x5BA2;&#x6237;&#x7AEF;-&#x670D;&#x52A1;&#x5668;&#xFF1B;&#x7F51;&#x7EDC;&#x901A;&#x4FE1;&#xFF1B;&#x670D;&#x52A1; \(gRPC+Protocol Buffers\)](.gitbook/assets/api_top_level.png)

* 5 个**立体灰度相机** \(Projected Stereo, D430?\)
* 12 个**自由度**，每条腿 3 个自由度 \(HX HY KN\)

![Spot](.gitbook/assets/spotanatomy.png)

## gRPC and Protocol Buffers

TODO

## 底层服务

* robot-id
* auth
* directory
* time-sync

## 几何与坐标系

![](.gitbook/assets/spotframes.png)

* Inertial frames
* The robot's body frame
* Sensor frames
* Object frames

## 机器人服务

* **estop**
* power
* robot-command
* robot-state
* image
* **local-grid**
* world-object

## 自主导航服务

Teach-Repeat/**Record\(a Map\)**-Replay

![&#x91C7;&#x7528;&#x300C;&#x5C40;&#x90E8;&#x5730;&#x56FE;+&#x62D3;&#x6251;&#x5730;&#x56FE;&#x300D;&#x5BFC;&#x822A;&#xFF0C;&#x56FE;&#x4E2D;&#x91C7;&#x7528;&#x300C;&#x4E8C;&#x7EF4;&#x7801;&#x300D;&#x521D;&#x59CB;&#x5316;&#x5B9A;&#x4F4D;](.gitbook/assets/tech_summary3.png)

**拓扑地图** \(Topological Graph\) **Graph = Waypoints + Edges, Waypoint 的作用等效于视觉 SLAM 中的关键帧**。

**Waypoints + Edges 的快照内容**

* Waypoint - 特征点，点云，AprilTag，图像，地面信息
* Edge - 两端点 Waypoint 之间的位姿变换，长度约为 2m，有无阶梯

Spot 自主导航未采用全局地图，Replay 阶段的地图不作更新。

总结：**Map** = **Graph + waypoint\_snapshots** + **edge\_snapshots**

![HF-Net](.gitbook/assets/pipeline.jpg)

💡用 Waypoints 附近的局部地图作视觉重定位 \(相对于某个 Waypoint 进行局部定位\)，具体参考 HF-Net。

### Mission 服务

**行为树**

## References

[波士顿动力 Spot 开箱概略](https://zhuanlan.zhihu.com/p/146362311)

[Spot SDK](https://github.com/boston-dynamics/spot-sdk)

[HF-Net: Robust Hierarchical Localization at Large Scale](https://github.com/ethz-asl/hfnet)

