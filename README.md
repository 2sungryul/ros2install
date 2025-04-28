# How to install ros2 foxy

OS : wsl2-ubuntu20.04

# Setup locale

$ sudo apt update && sudo apt install locales

$ sudo locale-gen en_US en_US.UTF-8

$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

$ export LANG=en_US.UTF-8

# setup source

$ sudo apt update && sudo apt install curl gnupg2 lsb-release

$ sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

# install ros2 package

$ sudo apt update

$ sudo apt install ros-foxy-desktop ros-foxy-rmw-fastrtps* ros-foxy-rmw-cyclonedds*
 
# install development tools

$ sudo apt update && sudo apt install -y build-essential cmake git libbullet-dev python3-colcon-common-extensions python3-flake8  python3-pip python3-pytest-cov python3-rosdep python3-setuptools python3-vcstool wget

$ python3 -m pip install -U argcomplete flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes pytest-repeat pytest-rerunfailures pytest

$ sudo apt install --no-install-recommends -y libasio-dev libtinyxml2-dev libcunit1-dev


# How to configure network for WSL2
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
