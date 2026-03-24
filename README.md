# Linux_setting
how to set linux for ubuntu version 24.04 in korean

### CUDA and CUDNN Installation
설치 설명 링크 <https://starlane.tistory.com/1>

### 설치 확인 코드
nvidia-smi (check whether the GPU is correctly detected)

nvcc --version or nvcc -V(check CUDA version)

cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2 (check cudnn version)

## 가상환경 설정 위한 것들

### 아나콘다 설치
설치 설명 링크 <https://osg.kr/archives/3899>

### 파이토치 설치

# Raisim 설치
설치 가이드 링크 <https://raisim.com/sections/Installation.html>

주의할 점: bashrc에 경로 지정해주고 source ~/.bashrc 해주기, 22.04에서 sudo ln -s /usr/lib/x86_64-linux-gnu/libdl.so.2 /usr/lib/x86_64-linux-gnu/libdl.so 하라고 되어있는데, 24.04에서도 해줘야 함. 22.04 이후 버전이라면 시행하기.

## Raisim 설치 이후에 빌드 후 runner 돌려서 시각화 하는 법
코드 작성 이후 vscode 상의 terminal이나, 동일한 위치(보통 ~/workspace/raisimGym: setup.py 있는 폴더)에서 python(3) setup.py develop -> python(3) raisimGymTorch/env/envs/raibo2/runner.py (괄호는 python으로 안되면 python3으로, runner.py가 있는 경로로 알아서 바꿔주면 됨)

(추가) 어차피 C++ executable 만들어서 pybind로 돌리는 것이기 때문에 그냥 rbuild 같은 빌드 명령어 쳐서 빌드 하고 runner.py 실행해도 됨.

추가로, runner.py에서 env.turn_on_visualization() 부분이 켜져야 매 iteration마다 시각화가 되는 것을 볼 수 있음 -> 학습 시간이 늘어나니까 일정 iteration마다 보게만 하거나, 아예 끄고 나중에 tester.py 코드 만들어서 보는 것을 추천.

### tester.py 만드는 법
runner.py를 돌리면 .pt 파일이 생성이 됨. 이렇게 생성된 .pt 파일의 주소를 복사해서 tester.py에 붙여 넣고 runner 돌리는 것처럼 tester를 돌리게 되면 학습이 아니라 테스트용 지형 및 설정된 조이스틱 명령을 따라서 돌아감. 기본적으로 B 키를 누르게 되면 env가 reset되면서 원점으로 돌아옴.

# Raisin 설치 및 켜는 법

### raisin 설치법
설치 가이드 링크 <https://github.com/raionrobotics/raisin_master>

install package 할 때 잘 안되면 repositories.yaml 눌러서 제목 따서 하나하나 다운로드 해주기.


### raisin 켜는 법
1. raisin_master 폴더에서 . ld_prefix_path.sh << 경로를 지정해주는 역할을 함. 여기서 update 어쩌고 뜨면 된 것

2. ./install/bin/raisin_gui 하면 창이 뜸. 이후로 터미널 하나 더 열어서 같은 위치에서 raisin_raibo2_node도 열기

3. 이 다음에 이름 클릭하고 연결 버튼 누르기 + 이후 조이스틱 추가 같이 생긴 버튼 누르기.

4. 턴 온 누르고 좀 기다리고 아래 있는 제어기 로드 하기.

5. 끌 때는 턴 오프 먼저 하고 기다린 후에 ctrl + c 해서 끄기

### raisin 처음 설치 시에 실행 과정 및 로봇 노드, 구이 켜는 법

전부 다 raisin_ws(raisin_master)

OTA에 ssh key 등록 : ssh-key gen -> enter 4번(passphrase 없이)
<br>
<br>
raisin_master clone 후에

python3 raisin.py install raisin_gui raisin_raibo2

python3 raisin.py setup 하고

install_dependencies.sh 실행

python3 raisin.py build -t release -i
<br>
<br>
**노드실행 : **

[sudo su]

source ld_prefix_path.sh

[nice -n 20] ./install/bin/raisin_raibo2_node [real] (sim이면 real을 빼고)
<br>
<br>
**구이 실행 : **

source ld_prefix_path.sh

./install/bin/raisin_gui

# 로봇에 새 제어기 올릴 때 어떻게 해야 하는지

plugin이나 이런 설정은 각 로봇의 환경에 맞게 세팅하면 되고, 전부 세팅이 완료되었으면 아래 과정을 따르면 됨.
 
학습된 제어기를 pt_to_txt.py를 이용해서 변환한 이후에 이 파일을 raibo_controller/raisin_blind_locomotion_controller/resource/donghoon(사용자명) 폴더 안에 넣고 params.yaml에서 제어기 경로를 변환 (network_path 수정)
 
이후에 python3 raisin.py build -t- release -i
 
이후 노드, 구이 실행하면 버전이 바뀐 제어기, 또는 새 제어기가 올라가 있을 것.
(주의할 점! : 새 제어기를 올릴 때에는 항상 호이스트에 연결 후 스탠드업 시키고 새 제어기를 로드할 것 (발산 방지), 주변에 사람이 없게 할 것.

# Vscode 좋은 extension
1. Nogic -> cmd + shift + P 한 이후에 Nogic:open visualizer 사용하면 코드의 흐름을 화살표로 잘 볼 수 있음. 

# RealSense Camera 사용법
기본 가이드 링크 <https://coding-ga-ding.tistory.com/179>

# 간단한 서버 사용법

docker run -it -e "DISPLAY=$DISPLAY" -e "QT_X11_NO_MITSHM=1" -e "XAUTHORITY=$XAUTH" -v "/tmp/.X11-unix:/tmp/.X11-unix:rw" -v ${PWD}/:/dataset --gpus all  --net=host --ipc=host --privileged --name [컨테이너로쓸이름] [이미지이름] 
: 이미지가 있고 , 컨테이너 화 해서 실행시킬때 쓰는명령어고
 
docker images : 현재 갖고 있는 도커 이미지들 보기 
docker ps :현재 실행되는 컨테이너 목록 보기 
docker ps -a : 진짜 다 있는 컨테이너 목록보기
 
컨테이너가 있긴 한데 컨테이너 종료  : docker start 컨테이너이름  <<- 컨테이너살아남 
docker stop <<- docker ps 에는 있엇는데 , 얘를 종료 시킬 수 있음 , docker ps -a 해야 보임.
 
docker attach 컨테이너이름 <<- docker ps 에 잇는 목록에 있는 컨테이너에 접속하기 
컨테이너 안에 있는데 나가고 싶어 : ctrl + D 나가지는 데 >> docker ps -a 해야 보임 (컴퓨터 끈거랑 동일) 
컨테이너 안에 있는데 컴퓨터 안 끄고 나가고 싶어 -> docker ps 만 쳐서 보이게싶어 :컴퓨터 끄기싫음: ctrl +p , q  

