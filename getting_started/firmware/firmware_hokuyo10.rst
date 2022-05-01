.. _doc_firmware_hokuyo10:

1. Hokuyo 10LX 이더넷 연결 설정
==========================================
.. note::
	USB로 연결하는 30LX 혹은 LIDAR를 사용한다면 이번 섹션은 넘어가도 된다.

**요구사항:**
	* 차량에 Hokuyo 10LX lidar 장착 완료
	* Pit/Host 노트북 혹은
	* 외부 모니터/디스플레이, HDMI 케이블, 키보드, 마우스

**예상 투입 시간:** 30 분

SSH나 유선 연결(모니터, 키보드, 마우스)로 Jetson NX에 연결하기

10LX를 사용하기 위해서 먼저 eth0 네트워크를 설정해야만 한다. 구입시 10LX에 ``192.168.0.10`` ip가 할당되어 있다. lidar에 subnet 0이다.

Jetson NX의 Linux GUI에서 **Network Configuration**을 연다. ipv4 탭에서 아래와 같이 etho0 port를 추가한다.

	* IP address ``192.168.0.15``
	* Subnet mask is ``255.255.255.0``
	* Gateway is ``192.168.0.1``

``Hokuyo`` 연결을 저장하고 GUI를 닫는다.

10LX에 연결할때 Hokuyo 연결이 선택되었는지 확인한다. 만약 모든 것이 제대로 설정되었다면 ``192.168.0.1`` 주소로 ping을 해보자.

.. image:: img/hokuyo1.gif
	:align: center
	:width: 200px
