# How to install ros2 foxy

OS : wsl2-ubuntu20.04

## Setup locale

$ sudo apt update && sudo apt install locales

$ sudo locale-gen en_US en_US.UTF-8

$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

$ export LANG=en_US.UTF-8

## setup source

$ sudo apt update && sudo apt install curl gnupg2 lsb-release

$ sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

## install ros2 package

$ sudo apt update

$ sudo apt install ros-foxy-desktop ros-foxy-rmw-fastrtps* ros-foxy-rmw-cyclonedds*
 
## install development tools

$ sudo apt update && sudo apt install -y build-essential cmake git libbullet-dev python3-colcon-common-extensions python3-flake8  python3-pip python3-pytest-cov python3-rosdep python3-setuptools python3-vcstool wget

$ python3 -m pip install -U argcomplete flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes pytest-repeat pytest-rerunfailures pytest

$ sudo apt install --no-install-recommends -y libasio-dev libtinyxml2-dev libcunit1-dev


# How to configure bridged networking mode for WSL2
1. 윈도우즈 검색창에 그룹정책편집 검색 또는 gpedit.msc 입력후 엔터

![image](https://github.com/user-attachments/assets/c7f1d5c6-77e4-46f4-b082-926672a985be)

2. 좌측창 -> 컴퓨터구성 -> 관리템플릿 -> 네트워크 -> Windows 연결관리자 -> 인터넷 또는 Windows 도메인에 대한 동시 연결수 최소화 -> 좌측 0 = 동시연결허용 설정 -> 확인

![image](https://github.com/user-attachments/assets/d58a6961-d2fb-4e98-accf-e1dfc3dd0aa5)

3. 윈도우즈 검색창에 hyper-v 관리자 검색 후 엔터

![image](https://github.com/user-attachments/assets/fab0310a-f988-4904-8adf-fc8c2ac67cc5)

4. 우측창의 가상스위치 관리자 클릭 -> 우측 가상스위치만들기 클릭

![image](https://github.com/user-attachments/assets/34540f5f-4f7b-4b19-8abc-13bf45af9ee2)

5. 가상스위치 만들기 메뉴에서 -> 이름 external, 연결형식은 외부 네트워크, 연결할 무선랜카드선택, 나머지는 선택하지 말것 -> 확인

![image](https://github.com/user-attachments/assets/838af903-03d3-49e9-9e54-7b42a6e024df)

6. 윈도우즈 설정 -> 네트워크 및 인터넷 -> 네트워크 브리지 생성 확인

![image](https://github.com/user-attachments/assets/95349d22-86b4-4ecd-92a0-5fe1e8700afe)

7. 윈도우즈 폴더 C:\Users\\<사용자id> 아래에 .wslconfig 이름의 텍스트 파일생성(확장자없어야함), 내용은 메모장열고 아래처럼 작성

![image](https://github.com/user-attachments/assets/81bddf53-3865-404c-b0a2-6700988e8177)

![image](https://github.com/user-attachments/assets/600b1e19-99b6-4458-91ff-b26079700a7f)

8. wsl2-ubuntu20.04 실행하고 ifconfig 명령실행하면 192.168.0.x 형식의 ip주소가 할당되어야 함 -> wsl2가 무선공유기에 직접 연결되었음을 의미

![image](https://github.com/user-attachments/assets/650ee692-d441-4e2d-a689-4e305a2827a4)

# How to configure mirrored networking mode for WSL2

mirrored networking mode 사용시에는 .wslconfig 파일의 내용을 다음처럼 수정

[WSL2]

networkingMode=mirrored

# How to install gstreamer on wsl2-Ubuntu20.04

$ sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio

## how to receive image from Jetson camera on wsl2-Ubuntu20.04

$ gst-launch-1.0 -v udpsrc port=8001 ! application/x-rtp,encoding-name=H264,payload=96 ! rtph2
64depay ! queue ! avdec_h264 ! videoconvert! autovideosink

## how to send camera image on Jetson nano

$ gst-launch-1.0 nvarguscamerasrc sensor-id=0 ! 'video/x-raw(memory:NVMM),format=NV12,width=640,height=360' ! nvvidconv flip-method=0 ! nvv4l2h264enc insert-sps-pps=true ! h264parse ! rtph264pay pt=96 ! udpsink host=192.168.0.19 port=8001 sync=false -q
