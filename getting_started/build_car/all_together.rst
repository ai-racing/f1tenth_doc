.. _doc_build_all_together:


1. 하나로 합치기
============================

상위 샤시에 자율주행 관련 컴포넌트를 붙이고 상위 샤시를 하위 샤시에 붙인다. 이 부분은 약간 어려울 수 있는데 그 이유는 전선과 케이블 때문이다. 최종 하드웨어 부품에 대한 최종 완료는 아래 비디오를 참고하자.

.. raw:: html

	<iframe width="560" height="315" src="https://www.youtube.com/embed/vNVFCq688ck" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


1. 상위 샤시를 하위 샤시에 붙이기
---------------------------------------------------------------
상위 샤시는 하위 샤시의 위에 스탠드오프로 연결한다. VESC는 차량의 뒷방향을 향해야 한다. 하위 샤시 PPM 케이블을 연결한다.

.. figure:: img/together/together_NX_00.JPG
	:align: center

	상위 샤시는 하위 샤시 위에 위치시킨다.


.. figure:: img/together/together02.JPG
	:align: center

	Lidar 케이블은 주의해서 배터리의 상단에 정리한다.

3개 M3 x 10mm 나사를 사용하여 하위 샤시에 있는 스탠드오프에 플랫폼 Deck을 장착한다.

lidar에서 플랫폼으로 USB 케이블을 안전하게 하기 위해서 케이블 타이를 이용하면 편리하다.

.. danger::
	The driveshaft that runs along the length of the chassis rotates when the car moves. You can manage the cables and wires in whatever manner you like but make sure that you keep them away from any rotating assemblies, including the driveshaft. If you don't, then the rotating assemblies will pull on all the cables and the last 1-2 hours of your life will have been in vain.

1. BLDC 모터를 VESC에 연결하기
----------------------------------------------
3개 4mm 3.5mm 불릿 어답터 Take three 4mm to 3.5mm bullet adapters.

.. figure:: img/together/together07.png
	:align: center

	4mm to 3.5mm bullet adapters.

BLDC의 파랑, 노랑, 흰색 전선을 아답터에 연결한다.

 .. figure:: img/together/together08.JPG
 	:align: center

	BLDC 모터에서 파랑, 노랑, 흰색 전선

VESC도 3개 전선에 대해서 **A**, **B**, **C** 라고 이름 붙인다.

 .. figure:: img/together/together10.jpg
  	:align: center

	VESCMKIII.

이제 VESC에 연결한다. 이 부분이 약간 어려울 수 있다.

	* **A** -> **흰색**
	* **B** -> **노랑**
	* **C** -> **파랑**

.. figure:: img/together/together09.JPG
  	:align: center

	BLDC 모터 전선을 Bullet 어답터에 연결하고 난 후에 VESC 전선에 연결한다.

.. important::
	VESC에 펌웨어를 플래쉬하고 난 후에 만약 차량이 예상과 달리 반대 방향으로 움직이면 흰색 전선을 "C"에 파란색 전선을 "A"로 연결을 바꿔주면 된다.


1. 배터리를 VESC와 연결하기
----------------------------

`충전 아답터 <https://www.amazon.com/gp/product/B078P9V99B/ref=crt_ewc_title_huc_1?ie=UTF8&psc=1&smid=A87AJ0MK8WLZZ>`_ 를 배터리 플러그에 연결

.. danger:: **충전 아답터랑 연결하는 경우 빨간색 전선은 빨간색에 검은색은 검은색에 제대로 연결해야 한다.** 반대로 연결하면 불이 날 수도 있다.

.. figure:: img/llchassis/llchassis15.JPG
	:align: center

	충전 아답터 케이블을 Lipo 배터리에 연결

다음으로 충전 아답터의 다른 쪽을 연결

.. figure:: img/llchassis/llchassis16.JPG
	:align: center

	XT90 아답터에 연결

연결하면 이렇게 된다.:

.. figure:: img/llchassis/llchassis17.JPG
	:align: center

	XT90 아답터 설치

배터리를 연결한 후 차량은 아래와 같다.

.. figure:: img/together/together_NX_01.JPG
	:align: center

	VESC에 연결된 배터리


1. NVIDIA Jetson NX을 VESC에 연결하기
----------------------------

NVIDIA Jetson NX은 파워보드에 연결이 필요하다. 보드는 2.5x5.5mm 전원잭
The NVIDIA Jetson NX needs to be connected to the powerboard. Use the barrel jack to pig tail connector. The board uses a 2.5x5.5mm power jack (MFN: PJ-036BH-SMT-TR). It is an unfortunate fact of life that the connections for barrel jacks are not standarized. For the specific barrel jack on this board, the center pin is POWER. Do not plug in a power supply whose center pin is ground. Connect one of the ends of the cable with GND on the powerboard, the other one with the 12V connector. Afterwards you can plug in the barrel jack in the NVIDIA Jetson NX.

.. figure:: img/together/together_NX_03.JPG
	:align: center

	NVIDIA Jetson power supply connected with the powerboard.

5. Lidar Connection
------------------------------

The lidar comes with two very long cables. We are going to try out best to manage them. Split the two cables of the lidar and loop them under the slots on the Platform Deck.

.. figure:: img/together/together_NX_06.JPG
	:align: center

	Storing the USB Lidar Cable in front of the Lidar

Using a twist tie, rubber band, or zip tie, gather the majority of the cables on each side. Then connect the Lidar to the NVIDIA Jetson. If using the UTM-30LX, plug the USB into one of the ports of the NVIDIA Jetson USB hub. If you are using a 10LX, plug it into the ethernet port of the Jetson NX.

Then its time to provide the energy connection for the Lidar. For the stripped cable side, insert the **BROWN (POWER)** and **BLUE (GROUND)** wires into one of the 12V terminal blocks on the Powerboard.

.. DANGER::
	***BROWN is POWER and BLUE is GROUND.*  DO NOT MIX THESE UP OTHERWISE YOU WILL FRY YOUR VERY EXPENSIVE LIDAR.** And then life will be very very sad. When in doubt, check the side of the Hokuyo. It will list out the correspondence of each wire.

.. figure:: img/ulchassis/ulchassis17.JPG
	:align: center

Lidar power is plugged into the terminal block with Brown to Power and Blue to Ground.


6. Attaching the PPM Cable
----------------------------
Now we are going to connect the PPM (Pulse-Position Modulation) cable to the Servo. The PPM cable connects the Servo to the VESC, which we will install on the Upper Level Chassis later.

.. figure:: img/llchassis/llchassis21.JPG
	:align: center

	PPM cable. Note that it has a white end and a black end.


Take 3 header pins,

.. figure:: img/llchassis/llchassis18.JPG
	:align: center

	Header pins.


Plug it into the servo wires.

.. figure:: img/llchassis/llchassis19.JPG
	:align: center

	Header pin connected to Servo cable of the Servo on the Traxxas chassis.


Connect the ppm cable with the servo wire.

.. danger::
	**BROWN is GROUND. It should be connected to the BLACK wire of the Servo Cable.** Make sure the polarity of the PPM cable to servo is correct.


.. figure:: img/llchassis/llchassis20.JPG
	:align: center

	PPM cable connected to Servo cable.

Now you can put everything together and plug it into the ppm slot on the VESC.

.. figure:: img/together/together_NX_04.JPG
	:align: center

	PPM cable plugged into VESC.

The Lower Level chassis is now set up and we can move on to the autonomy elements. First accomplishment completed!

.. figure:: img/llchassis/llchassis22.gif
  :align: center


7. Final Touches
------------------------------
Almost there!

Connect a micro USB (here: the white cable) from the VESC to the USB hub.

.. figure:: img/together/together_NX_08.JPG
  	:align: center

	Micro USB plugged into the VESC. Plug the USB side into the USB hub.

Finally, screw on the antennas included with the Jetson TX2 Kit to the Antenna Terminals.

8. Voila!
----------
Your final vehicle should look like the following:

.. figure:: img/together/final.JPG
   :align: center

	Final product! It looks a bit messy but cable management is an art!


Now we're ready to start driving!

.. figure:: img/together/together05.gif
   :align: center
   :width: 300px

DEPRECATED: NVIDIA TX2 Setup
----------

Attach the two wires for the Jetson Wi-Fi antenna to the two gold-colored connectors near the fan connector on the heat sink (the order of the wires doesn’t matter). This can be a little tricky, so you might want to use a flathead screwdriver to ensure the connections are tight. ​ Don’t press too hard​ , however as you can easily damage the connectors if you use excessive force!

.. figure:: img/together/together05.JPG
  	:align: center

	Attached antenna wires.
