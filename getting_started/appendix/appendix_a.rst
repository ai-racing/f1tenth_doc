.. _doc_appendix_A:

Appendix A: 호스트와 VM 간에 공유하는 폴더들
=================================================
Ubuntu를 실행하는 호스트 컴퓨터가 없다면 VM(Virtual Machine)을 사용해서 위에 과정을 진행해야 한다. 만약 이런 경우라면 호스트(노트북의 기본 OS)와 게스트(VM상에서 실행되는 Ubuntu) 사이에 폴더를 공유하도록 설정하면 편리하다.

호스트는 맥 OS X El Capitan(다른 맥 OS도 동일)과 Virtualbox에서 Ubuntu 16.04 게스트에 대해서 다음과 같이 진행한다.

이미 호스트 컴퓨터에 Virtualbox가 설치되어 있다고 가정하고 여기서 Ubuntu 16.04가 설치되어 있다. 더 자세한 내용은 온라인을 참조할 수 있으며 여기서는 설정하는 한가지 방법을 소개한다.

#. 호스트에서 공유를 원하는 폴더를 생성한다. 이를 sfVM이라 부르고 ``~/sfVM``에 있다고 가정한다.
#. VirtualBox를 구동시킨다.
#. Ubuntu VM을 선택한다.
#. *Settings* -> *Shared Folders* -> ‘+’ 표시 클릭 -> 위에서 생성한 sfVM으로 이동. **Auto-mount**와 **Make permanent**를 확인.
#. VM 구동시킨다.
#. Guest를 설치 : VBox 메뉴에서  *Devices* -> *Install Guest Additions* -> ... ->
#. SW 실행
#. 수동으로 공유 폴더를 마운트 시킨다. 다음을 실행:
	.. code:: bash

		$​ mkdir ~/guest_sfVM (or whatever you want to call it)
		$​ id
		uid=1000(houssam) gid=1000(houssam)
		$​ sudo mount -t vboxsf -o uid=1000,gid=1000 sfVM ~/guest_sfVM

#. 호스트에서 잘 동작하는지 확인하기 위해서 ``~/sfVM`` 공유 폴더에 파일을 넣어본다. 그리고 게스트에서 ``~/guest_sfVM``에 파일이 보이지는 확인한다.