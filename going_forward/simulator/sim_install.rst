Linux/ROS 설치
============================

시뮬레이터는 ROS을 사용하므로 Ubuntu Linux가 설치된 PC가 필요하다. Ubuntu 20.04 버전과 ROS Noetic이 필요하다. 설치에 관한 정보는 `<http://wiki.ros.org/noetic/Installation>`_ 를 참고하자.

의존성
------------------
다음과 같은 의존성을 가진다:
  
  - tf2_geometry_msgs
  - ackermann_msgs
  - joy
  - map_server

설치 방법

.. code-block:: bash
  
  sudo apt-get install ros-noetic-tf2-geometry-msgs ros-melodic-ackermann-msgs ros-melodic-joy ros-melodic-map-server

의존하는 전체 목록은 ``package.xml`` 파일에서 확인할 수 있다.

패키지(Package)
------------
시뮬레이터 패키지를 설치하기 위해서 시뮬레이터 저장소를 여러분의 catkin workspace에 clone한다. :

.. code-block:: bash

  cd ~/catkin_ws/src
  git clone https://github.com/f1tenth/f1tenth_simulator.git

다음으로 build하기 위해서 catkin_make를 실행:

.. code-block:: bash

  cd ~/catkin_ws
  catkin_make
  source devel/setup.bash

바로 시작하기
---------------
시뮬레이터를 실행하기 위해서 아래를 실행:

.. code-block:: bash

  roslaunch f1tenth_simulator simulator.launch

시뮬레이션에 필요한 모든 것들을 launch 시킨다. : roscore, 시뮬레이터, map, 레이싱카 모델, 조이스틱 서버

.. figure:: img/sim_install.png
  :align: center

  시뮬레이션이 실행되었다.

