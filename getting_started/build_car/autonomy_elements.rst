.. _doc_build_autonomy_elements:


2. Autonomy Elements
======================
In the second part of the hardware setup we start preparing the autonomy elements for our F1TENTH car. The complete process for the second hardware part can be watched in this video tutorial too.

.. raw:: html

	<iframe width="560" height="315" src="https://www.youtube.com/embed/L-V-0zzkl10" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

1. NVIDIA Jetson NX 준비하기
---------------------------------
NVIDIA Jetson NX를 구입하면 작은 플라스틱 개발 보드가 붙어져 있다. 차량에서 이를 사용하기 위해서 Jetson NX와 Wi-Fi 안테나를 개발보드에서 나사를 풀어야 한다. 먼저 NVIDIA Jetson NX를 박스에서 꺼내보자.

.. figure:: img/autonomy/autonomy12.JPG
	:align: center

	NVIDIA Jetson NX 언박싱


위에서 Jetson NX를 보면 4개의 나사가 있다.(이미지에서 빨간 원) 4개 나사를 모두 풀도록 한다.

.. figure:: img/autonomy/autonomy13.JPG
	:align: center

	NVIDIA NX에 장착된 플라스틱 보드의 나사를 제거


Jetson NX를 뒤집어보자. 안테나 케이블 때문에 플라스틱 보드가 여전히 붙어 있는 것을 볼 수 있다.

.. figure:: img/autonomy/autonomy14.JPG
	:align: center

	NVIDIA NX에 붙어 있는 플라스틱 개발 보드


2개 안테나 케이블이 Jetson NX에 고정되어 있다. 모두 풀어준다. 손톱이나 납작한 드라이버를 사용해서 들어올린다.

.. figure:: img/autonomy/autonomy15.JPG
	:align: center

	NVIDIA Jetson NX의 2개 안테나를 제거


NVIDIA Jetson NX를 개발보드에서 분리한다. 플랫폼 판에 연결할 수 있다.

.. figure:: img/autonomy/autonomy16.JPG
	:align: center

	NVIDIA Jetson NX를 개발 보드에서 분리하기


1. WiFi 안테나 준비하기
---------------------------------
다음 단계로 
In the next step we are providing both Wifi Antennas so we can mount them in the later steps quick and easy. First of all unpackage your antennas and demount the cables from the antennas. Remove the two brass-colored nuts holding the antennas to the L-shaped bracket, and then remove the two antennas from the bracket.

.. figure:: img/autonomy/autonomy11.png
	:align: center

	Demounted Wifi antennas

Afterwards we need to Screw the Standoffs onto the antenna bracket. Using a Phillips screwdriver, thread the two screws you saved earlier completely into the bracket as pictured below. Attach two M3 FF 45mm standoffs to the opposite ends of the screws and hand-tighten them until they won’t turn anymore. Use the pliers to tighten the standoffs more while you hold the head of the screw in place using the screwdriver.

.. figure:: img/autonomy/autonomy08.png
	:align: center

	Screwing standoffs onto the bracket.

Once you’ve done these steps, place the antennas and washers back into the bracket, and tighten the brass nuts onto the threaded connectors again.
It helps to use two pairs of pliers: one to hold the rear nuts in place and another to unscrew the nuts on the end with the antenna connectors.

.. figure:: img/autonomy/autonomy07.png
	:align: center

	Thighten the nuts from the L-shaped bracked.

We can now move on to mounting all of the autonomy elements onto the Upper Level Chassis in the next section. Second accomplishment completed.

.. figure:: img/autonomy/autonomy10.gif
	   :align: center


DEPRECATED: Preparing the NVIDIA Jetson TX2
---------------------------------
In this section we are describing how to use the NVIDIA Jetson TX2 as a main ECU for the F1TENTH vehicle. This setup is deprecated and no longer recommended.

**1. Removing the NVIDIA Jetson TX2 Developer Board**

When you purchase a Jetson TX2, it is attached to a development board. In order to use it on the car, you will need to unscrew the Jetson TX2 and its Wi-Fi antenna from the development board.

Before you remove the antenna, you will need to remove the bottom plate from the development board. Remove the four screws marked below and lift the development board away from the plate.

.. figure:: img/autonomy/autonomy05.png
	:align: center

	TX2 still in its development board. Remove the four circled screws.


Next, remove the Wi-Fi antenna by unscrewing the two screws marked below. Keep the screws in a safe place, as you’ll use them in a bit to attach the antennas to standoffs.

.. figure:: img/autonomy/autonomy06.png
	:align: center

	Remove the antenna by unscrewing the two circled screws.


Remove the two brass-colored nuts holding the antennas to the L-shaped bracket, and then remove the two antennas from the bracket. It helps to use two pairs of pliers: one to hold the rear nuts in place and another to unscrew the nuts on the end with the antenna connectors.

.. figure:: img/autonomy/autonomy07.png
	:align: center

	Removing nuts from the L-shaped bracked.


Using a Phillips screwdriver, thread the two screws you saved earlier completely into the bracket as pictured below. Attach two M3 FF 45mm standoffs to the opposite ends of the screws and hand-tighten them until they won’t turn anymore. Use the pliers to tighten the standoffs more while you hold the head of the screw in place using the screwdriver. Once you’ve done these steps, place the antennas and washers back into the bracket, and tighten the brass nuts onto the threaded connectors again.

.. figure:: img/autonomy/autonomy08.png
	:align: center

	Screwing standoffs onto the bracket.


Unplug the Jetson TX2’s fan and remove the Jetson TX2 from the development board by using a T3 Torx screwdriver to unscrew the Jetson TX2 (the large silver heat sink), and then pull up gently to detach it from the development board. Keep the Jetson TX2 in a safe place while you attach the antennas to the power board.

.. figure:: img/autonomy/autonomy09.png
	:align: center

	Unplugging and removing the Jetson TX2's fan.


**2. Attaching the Orbitty to the TX2**

Seat the TX2 Module connector to the Orbitty board connector like so:

.. figure:: img/autonomy/autonomy01.JPG
	:align: center

	Attach the Orbitty Carrier Board to the TX2.

Put an M3 x 20mm screw through one of the Orbitty mount holes followed by one 8mm nylon spacer then 35mm FF M3 standoffs.  Repeat for the remaining three mounting holes.

.. figure:: img/autonomy/autonomy02.JPG
	:align: center

	Screw, spacer, and standoff mounted.

The results should look like this:

.. figure:: img/autonomy/autonomy03.JPG
	:align: center

	Orbitty Carrier board mounted on top of TX2 with standoffs attached.

Plug the TX2 fan connector into the Orbitty board.

.. figure:: img/autonomy/autonomy04.JPG
	:align: center

	Plugging the Jetson's fan to the Orbitty board.
