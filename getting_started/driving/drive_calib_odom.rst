.. _doc_calib_odom:

Odometry 칼리브레이션하기
=========================
.. note:: 이 섹션에서는 :ref:`Building the Car <doc_build_car>`, :ref:`System Configuration <doc_software_setup>`, :ref:`Installing Firmware <doc_build_car_firmware>`, :ref:`Driving the Car <doc_drive>` 를 완료했다고 가정한다.

마지막 단계

**요구사항:**
	* 완전히 조립된 차량
	* Pit/Host 컴퓨터
	* Logitech F710 조이스틱
	* Tape measure

**난이도:** 중간

**예상 투입 시간:** 1 시간

만들기, 설정, 설치가 완료되고 나면 차량의 odometry 칼리브레이션이 필요하다.
VESC는 m/s 단위의 속도와 radians 단위의 조향각을 입력으로 받는다. 모터와 서보는 RPM(revolution per minute)와 서보 위치가 필요하다. 차량에 따라 변환된 파라미터가 필요하다.

#. `vesc.yaml <https://github.com/f1tenth/f1tenth_system/blob/master/racecar/racecar/config/racecar-v2/vesc.yaml>`_ 파라미터로 칼리브레이션이 필요하다.

#. 가이드 : `Tuning Guide <https://mushr.io/tutorials/tuning/>`_  `Mushr <https://mushr.io/about/>`_ 
