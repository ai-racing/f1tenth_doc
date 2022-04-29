시뮬레이터 사용하기
====================

드라이빙
-----------------
레이싱카를 키보드를 사용하여 수동으로 조정해보자. 조정하기 위서 키보드의 ``K`` 키를 누르면 터미널에서 다음과 같이 보인다.:


.. figure:: img/sim_keyboard.png
  :align: center

다음으로 표준 WASD 키를 사용하여 조정:

	- ``W`` 차량 전진
	- ``A`` 핸들 왼쪽으로
	- ``S`` 차량 후진
	- ``D`` 핸들 오른쪽으로

``스페이스바``를 눌러서 차량 멈추기

.. note::

	Be aware that if you crash, the keyboard will be turned off, and you’ll have to press ``K`` again to turn it back on. Also, it can only handle one key press at a time, so holding down multiple keys at once does not work. Lastly, pressing ``A`` or ``D`` will steer to a fixed angle, and the only way to straighten out is with ``spacebar``.

The controls are a bit tricky, but hopefully you won't have to do too much manual driving!

If you are using a joystick, make sure the correct axis is set in params.yaml for steering and acceleration- this changes between different joysticks.

.. figure:: img/sim_keyboard2.gif
	:align: center

Instant Pose Setting
-----------------------
A useful function of the simulator is that you can instantly move the car without driving it to its new location. To do this, click the ``2D Pose Estimate`` pose button at the top of the rViz window, and then click the desired location on the track to move the car there.

.. figure:: img/sim_pose.gif
  :align: center