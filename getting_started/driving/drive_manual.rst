.. _drive_manualcontrol:

수동 조정
=================
**요구사항:**
	* 완성된 차량
	* Pit/Host 컴퓨터
	* Logitech F710 조이스틱

**대략 소요 시간:** 30 분 - ∞ 재밌으면 더 많은 시간을 쓸수 있다!

개요
------------
차량이 스스로 운전하게 하기 전에 사람이 직접 운전하는 것이 제대로 동작하는지 테스트해야 한다. VESC나 차의 구동 부품(모터나 기어)을 교체한 경우 수동으로 조정해보자. 사전에 이런 작업을 해두면 나중에 코드가 동작하지 않는 경우 하위 하드웨어 이슈를 제외하고 디버깅을 할 수 있다.

**이 섹션에서 TX2에 연결하는 경우 SSH를 이용해야만 한다.**

1. 차량 검사
-----------------------
시작하기 전에 많은 사고를 최소화하기 위해서 먼저 차량을 검사하자. 

#. 차량에서 LIPO 배터리를 분리한다.
#. **Logitech Joypad**의 USB 동글 수신기를 **USB hub**에 연결하자.
#. VESC를 연결한다.
#. 차량과 노트북 모두 공유기에 연결한다. :ref:`System Configuration <doc_software_setup>`.
#. `f110_system`` 저장소를 clone하고 :ref:`previous section <doc_drive_workspace>` 에서 설명한 작업 디렉토리를 설정한다
#. 이 섹션에서는 ``tmux`` 프로그램을 사용하여 하나의 SSH 연결에서 여러 터미널을 실행시킬 수 있다. 만약 GUI가 더 좋다면 VNC를 사용할 수도 있다.

1. 차량 운전하기
----------------------
#. Open a terminal on the **Pit** laptop and SSH into the car from your computer.
#. Once you’re in, open a terminal window and run ​``$tmux`` so that you can spawn new terminal sessions over the same SSH connection.
#. In your tmux session, spawn a new window (using ``Ctrl-B`` and then ``C``) and run ​``$roscore``​ to start ROS.
#. Navigate to other free terminal using ``Ctrl-B`` and then ``P`` or ``N`` by switch to previous or next session, or using ``Ctrl-B`` and then the number of the session, navigate to your workspace that we set up before, run ``$ catkin_make`` and source the directory using ``$ source devel/setup.bash``.
#. Run ``$ roslaunch racecar teleop.launch​`` to launch the car. 
	* If you see an error like this: ``[ERROR] [1541708274.096842680]: Couldn't open joystick force feedback!`` It means that the joystick is connected. 
	* If this gives you a segmentation error and it’s caused by compiling the joy package (which you can check by running the joy node on its own), this could be because you are using the joy package from the ROS distribution (i.e., installed with apt-get). Remove that by ``sudo apt-get remove joy`` and ``catkin_make`` in your workspace, and sourcing the setup bash again. This should compile and use the joy package that’s in the repo.

#. Hold the LB button on the controller to start controlling the car. Use the left joystick to move the car forward and backward and the right joystick for steering.
	
	* If nothing happens or if the right joystick is not mapped to steering, your might joystick might be in a different mode, press the *mode* button to change the mode.
	* If nothing happens, one reason can be that the ``joy_node`` is listening for inputs on the ``js0`` port, but the operating system has assigned a different port to it, like ``js1``. Edit the ``yaml`` file which specifies which port to listen to. You can tell what file that is by reading the launch file (and following the call tree to other launch files).
	* Note that the LB button acts as a “dead man’s switch,” as releasing it will stop the car. This is for safety in case your car gets out of control.
	* You can see a mapping of all controls used by the car in ``f110_system/racecar/racecar/config/racecar-v2/joy_teleop.yaml``. For example, in the default configuration, axis 1 (left joystick’s vertical axis) is used for throttle, and axis 2 (right joystick’s horizontal axis) is used for steering. If you need to check which axis correspond to what buttons/axis on the joystick, run the joy node, when the joystick is connected, you can see the index of the button/axis that's changed.

Troubleshooting
------------------
Here are some common errors:

* **VESC out of sync errors**: Check that the VESC is connected. If the error persists, make sure you're using the right VESC driver node. Currently, the ``vesc`` package in the f110_system repo only supports VESC 6+. If you have an older implementation of VESC (for example the FOCBox), use the repo `here <https://github.com/mit-racecar/vesc>`_ instead.
* **Serial port busy errors**: Your VESC might have just booted up, give it a few seconds and try again.
* **SerialException errors** ​and you’re using the 30LX Hokuyo​, the errors might be due to a port conflict: e.g., suppose that the lidar was assigned the (virtual serial bi-directional) port ``ttyACM0`` by the operating system. And suppose that the ``vesc_node`` is told the VESC is connected to port ``ttyACM0`` (as per ``vesc.yaml``). Then when the ``vesc_node`` receives joystick commands from ``joy_node`` (via ROS), it pushes them to ``ACM0`` - so these messages actually go to the lidar, and the VESC gets garbage back. So change the ``vesc.yaml`` port entry to ``ttyACM1``. (This whole discussion remains valid if you switch 0 and 1, i.e. if the OS assigned ACM1 to the lidar and your ``vesc.yaml`` lists ACM1). Note that everytime you power down and up, the OS will assign ports from scratch, which might again break your config files. So a better solution is to use udev rules, as explained in `this <firmware.html#udev-rules-setup>`_ section​. (See the source code of joy node for the default port for the joystick. You can over-ride that using a parameter in the launch file. See the joy documentation for what parameter that is).
* **urg_node related errors**: Check the ports (e.g. an ip address in sensors.yaml can only be used by 10LX, not 30LX, and vice-versa for the /dev/ttyACM​n​).
* **razor_imu errors**: Delete the IMU entry from the launch file - we’re not using an IMU in this build.

Congratulations on building the car, configuring the system, installing the firmware, and driving the car! You've come a long way. Pat yourself on the back and high five your other hand. You can head over to `Learn <https://f1tenth.org/learn.html>`_ and try out some of the labs there.

.. image:: img/drive02.gif
	:align: center
	:width: 300px

