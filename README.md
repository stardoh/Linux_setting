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


# Raisin 설치 및 켜는 법

### raisin 설치법
설치 가이드 링크 <https://github.com/raionrobotics/raisin_master>

install package 할 때 잘 안되면 requirement.txt 눌러서 제목 따서 하나하나 다운로드 해주기.


### raisin 켜는 법
1. raisin_master 폴더에서 . ld_prefix_path.sh << 경로를 지정해주는 역할을 함. 여기서 update 어쩌고 뜨면 된 것

2. ./install/bin/raisin_gui 하면 창이 뜸. 이후로 터미널 하나 더 열어서 같은 위치에서 raisin_raibo2_node도 열기

3. 이 다음에 이름 클릭하고 연결 버튼 누르기 + 이후 조이스틱 추가 같이 생긴 버튼 누르기.

4. 턴 온 누르고 좀 기다리고 아래 있는 제어기 로드 하기.

5. 끌 때는 턴 오프 먼저 하고 기다린 후에 ctrl + c 해서 끄기

