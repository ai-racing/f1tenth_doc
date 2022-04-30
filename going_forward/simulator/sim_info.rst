추가 정보
=======================

RVIZ 시각화
-----------------------
시뮬레이터가 실행시키고 rviz를 연다.
왼쪽 아래에 ``Add`` 버튼을 클릭하고 ``By topic`` 탭에 ``/map`` topic과 ``/scan`` topic을 추가한다.
다음으로 ``By display type`` 탭에서 RobotModel 타입을 추가한다.
새로 추가한 LaserScan 섹션에 있는 왼쪽 패널에 size를 0.1미터로 변경하여 lidar가 선명하게 보이도록 한다.(레인보우로 보여짐)

차량을 조정하기 위해서 키보드나 USB 조이스틱을 사용하거나 ``2D Pose Estimate 버튼``을 클릭하여 차량을 원하는 위치로 드래그하여 위치시킬 수 있다.

ROS API
------------------------
시뮬레이터의 2가지 목적은 실제 차량을 시뮬레이션하고 빠르게 레이싱 알고리즘을 프로토타이핑할 수 있다는 것이다. **simulator** node는 만약 모든 topic 이름을 그대로 사용한다면 ai-car 차량을 대체하여 운전할 수 있다. ROS 나머지 node들은 잘 구성하면 새로운 planning 알고리즘을 빠르게 추가하고 운행 중에도 변경이 가능하다.

.. figure:: img/sim_graph_public.png
	:align: center

	ROS nodes의 간략화한 그래프

공개한 시뮬레이터에 planning node가 어떤 형태여야 하는지 보여주기 위해서 간단한 **random driver** node가 제공한다. 각 planner는 **simulator**가 publish하는 센서 데이터를 수신하고 난 후에 `AckermannDrive <http://docs.ros.org/melodic/api/ackermann_msgs/html/msg/AckermannDrive.html>`_ 메시지를 자신의 특정 topic (e.g., ``/random_drive``)으로 publish한다. **mux** node는 이런 topic들 모두를 listen하고 난 후에 동작하는 planner로부터 메시지를 가지고 main ``/drive`` topic으로 이를 publish한다. 메시지 내부에 있는 속도(velocity)와 조향각(steering angle)만 사용된다. **mux** node는 조이스틱과 키보드 메시지도 listen하여 수동 조정이 가능하다.
**behavior controller** node는 **mux** node에게 어떤 planner가 ``/mux`` topic을 거치는지 알려준다. 기본적으로 각 planner는(키보드와 조이스틱 포함) 조이스틱 버튼과 키보드 키로 매핑되고 간단하게 수동으로 켜고 끄기가 된다.
추가로 충돌시에는 차량이 멈추고 모든 mux 채널은 초기화된어 제어가 되지 않게 된다.

순간적으로 차량을 새로운 상태로 이동시키기 위해서 `Pose <http://docs.ros.org/melodic/api/geometry_msgs/html/msg/Pose.html>`_ 메시지를 ``/pose`` topic으로 publish한다. 이것은 연속된 자동화된 테스트를 하는데 유용할 수 있다.

시뮬레이션된 lidar는 ``/scan`` topic을 `LaserScan <http://docs.ros.org/melodic/api/sensor_msgs/html/msg/LaserScan.html>`_ 메시지로 publish한다.

차량의 pose는 ``map`` frame과 ``base_link`` frame 사이에 변환으로 broadcast된다. ``base_link``는 rear axis의 중심이다. ``laser`` frame는 lidar scan이 가지는 frame을 정의하며 다른 transform은 ``base_link`` 사이를 broadcast한다.

Behavior Controller 변경하기
---------------------------------
키보드, 조이스틱, 직접 pose 제어 이외에 차량의 behavior를 변경하고자 한다면 새로운 planning node와 **behavior controller** node에 새로운 코드를 작성해야한다. 새로운 planner를 추가하기 위한 단계들에 대해서 알아보자. 기본적으로 **behavior controller**는 센서 메시지를 listen하고 레이싱을 하는 동안 입력에 따라서 planner를 자동으로 변경하는 차량을 위한 제어기를 직접 작성할 수 있다.

planning node 추가하기
^^^^^^^^^^^^^^^^^^^^^^^
새로운 planner node를 추가하는데 필요한 여러 단계가 있다. 정확히 무엇을 해야하는지 
There are several steps that necessary to adding a new planning node. There is commented out code in each place that details exactly what to do. Here are the steps:

#. Make a new node that publishes to a new drive topic. Look at `random_walk.cpp <https://github.com/f1tenth/f1tenth_simulator/blob/master/node/random_walk.cpp>`_ for an example
#. Launch the node in the launch file ``simulator.launch``
#. Make a new ``Channel`` instance at the end of the Mux() constructor in ``mux.cpp``
#. Add if statement to the end of the joystick and keyboard callbacks (key\_callback(), joy\_callback) in ``behavior_controller.cpp``
#. In ``params.yaml``, add the following:

	* a new drive topic name
	* a new mux index
	* a new keyboard character (must be a single alphabet letter)
	* a new joystick button index

You'll need to get the mux index and drive topic name in ``mux.cpp`` for the new ``Channel``, and the keyboard character, mux index, and joystick button index will all need to be added as member variables in ``behavior_controller.cpp``. Your planning node will obviously need the drive topic name as well.

Parameters
----------------
The parameters listed below can be modified in the ``params.yaml`` file.

Topics
^^^^^^^^^^^
``drive_topic``: The topic to listen to for autonomous driving.

``joy_topic``: The topic to listen to for joystick commands.

``map_topic``: The topic to listen to for maps to use for the simulated scan.

``pose_topic``: The topic to listen to for instantly setting the position of the car.

``pose_rviz_topic``: The topic to listen to for instantly setting the position of the car with Rviz's "2D Pose Estimate" tool.

``scan_topic``: The topic to publish the simulated scan to.

``distance_transform_topic``: The topic to publish a distance transform to for visualization (see the implementation section below).


Frames
^^^^^^^^^^
``base_link``: The frame of the car, specifically the center of the rear axle.

``scan_frame``: The frame of the lidar.

``map_frame``: The frame of the map.


Simulator Parameters
^^^^^^^^^^^^^^^^^^^^^^^
``update_pose_rate``: The rate at which the simulator will publish the pose of the car and simulated scan, measured in seconds. Since the dynamics of the system are evaluated analytically, this won't effect the dynamics of the system, however it will effect how often the pose of the car reflects a change in the control input.

Car Parameters
^^^^^^^^^^^^^^^^^^
``wheelbase``: The distance between the front and rear axle of the racecar, measured in meters. As this distance grows the minimum turning radius of the car increases.

``width``: Width of car in meters

``max_speed``: The maximum speed of the car in meters per second.

``max_steering_angle``: The maximum steering angle of the car in radians.

``max_accel``: The maximum acceleration of the car in meters per second squared.

``max_steering_vel``: The maximum steering angle velocity of the car in radians per second.

``friction_coeff``: Coefficient of friction between wheels and ground

``mass``: Mass of car in kilograms


Lidar Parameters
^^^^^^^^^^^^^^^^^^^^
``scan_beams``: The number of beams in the scan.

``scan_field_of_view``: The field of view of the lidar, measured in radians. The beams are distributed uniformly throughout this field of view with the first beam being at ``-scan_field_of_view`` and the last beam being at ``scan_field_of_view``. The center of the field of view is direction the racecar is facing.

``scan_distance_to_base_link``: The distance from the lidar to the center of the rear axle (base_link), measured in meters.

``scan_std_dev``: The ammount of noise applied to the lidar measuredments. The noise is gaussian and centered around the correct measurement with standard deviation ``scan_std_dev``, measured in meters.

``map_free_threshold``: The probability threshold for points in the map to be considered "free". This parameter is used to determine what points the simulated scan hits and what points it passes through.

Joystick Parameters
^^^^^^^^^^^^^^^^^^^^^
``joy``: This boolean parameter enables the joystick if true.

``joy_speed_axis``: The index of the joystick axis used to control the speed of the car. To determine this parameter it may be useful to print out the joystick messages with ``rostopic echo /joy``.

``joy_angle_axis``: The index of the joystick axis used to control the angle of the car.  To determine this parameter it may be useful to print out the joystick messages with ``rostopic echo /joy``.

``joy_button_idx``: The index of the joystick button used to turn on/off joystick driving.

