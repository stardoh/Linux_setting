# Linux_setting
how to set linux for ubuntu version 24.04 in korean

### CUDA and CUDNN Installation
설치 설명 링크 <https://starlane.tistory.com/1>

### 설치 확인 코드
nvidia-smi (check whether the GPU is correctly detected)

nvcc --version or nvcc -V(check CUDA version)

cat /usr/local/cuda/include/cudnn_version.h | grep CUDNN_MAJOR -A 2 (check cudnn version)
