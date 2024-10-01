<b> Getting Started with AI on Jetson Nano

```
 1. Jetson Nano Setting 준비물
  
        - jetson nano 4gb


  
        - c type power adapter
  
        - 와이파이 동글
  
        - 웹캠(USB Camera), 또는 CSI Camera (라즈베리파이 V2)
  
        - 64기가 이상 마이크로sd카드
  
        - 그외 쿨링펜, lcd, 또는 모니터. hdmi
```
<b>

![jetson](https://github.com/user-attachments/assets/fadbd75e-5c73-4563-ac8d-f6779e17bcb3)
![jetson_exp](https://github.com/user-attachments/assets/c3ef7062-308c-4118-947c-35479fbd2581)

<b> 2. jetson nano에 대하여

<b>  welcome 부터 따라하기
       https://learn.nvidia.com/courses/course?course_id=course-v1:DLI+S-RX-02+V2&unit=block-v1:DLI+S-RX-02+V2+type@vertical+block@aba5104413ae454c8c63a6f301925337

<b> 3. jetpack downloads 

<b>      https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write

<b> 4. 이미지  굽기 위해 필요한 것들.

       4-1. sd card formatter ---> download
       4-2. balenaetcher download --->  이미지 굽기
       4-3. 제슨나노에 sd넣고 우분투 설치

  #####     
     
<b> 5. 쿨링팬 설치
``` bash
sudo sh -c 'echo 128 > /sys/devices/pwm-fan/target_pwm'
```
<b>  6. usb-camera  얼굴의 코 눈 인식하는 것도 해봄, 이미지 캡쳐와 영상 녹화 cctv기능 구현 j는 이미지 캡쳐, 1은 영상 녹화 시작 0은 영상녹화 스톱
```
git clone https://github.com/jetsonhacks/USB-Camera.git
cd USB-Camera
ls
python3 usb-camera-gst.py 
python3  face-detect-usb.py
nvgstcapture-1.0 --mode=1 --camsrc=0 --cap-dev-node=0
j
nvgstcapture-1.0 --mode=2 --camsrc=0 --cap-dev-node=0
1
0
```
#####  이곳에 사진 넣고 영상 넣을 것  참고 링크 https://ndb796.tistory.com/557


<b>  7. 한글 설치 , reboot 한 후 오른쪽 하단 키보드 모양을 오른쪽 마우스 클릭→ configure click
```
참고 링크 https://driz2le.tistory.com/253
```
```
sudo apt-get update
sudo apt-get install fcitx-hangul
reboot
```
       
<b> 8. 제슨 알아보고 설치하기
  
  [https://developer.nvidia.com/embedded/learn/jetson-nano-2gb-devkit-user-guide#id-.JetsonNano2GBDeveloperKitUserGuidevbatuu_v1.0-DeveloperKitSetup](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write)
<b> image classification 준비
```
dli@dli-desktop:~$ mkdir -p ~/nvdli-data
dli@dli-desktop:~$ sudo docker run --runtime nvidia -it --rm --network host \
>     --memory=500M --memory-swap=4G \
>     --volume ~/nvdli-data:/nvdli-nano/data \
>     --volume /tmp/argus_socket:/tmp/argus_socket \
>     --device /dev/video0 \
>     nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1kr
```
<b>  결과 
[sudo] password for dli: 
Unable to find image 'nvcr.io/nvidia/dli/dli-nano-ai:v2.0.2-r32.7.1kr' locally
v2.0.2-r32.7.1kr: Pulling from nvidia/dli/dli-nano-ai
f46992f278c2: Pulling fs layer 
d0ec296fcb76: Pulling fs layer 
9e18ddc8ca7a: Pulling fs layer 
457ba495c8e5: Waiting 
71bca45e35bd: Waiting 
644761cdc735: Waiting 
11628dbc31eb: Waiting 
d364c3700c33: Waiting 
01869d070b2e: Waiting 
cc3009375042: Pulling fs layer 
3e182d6364dc: Pulling fs layer 
f72feb4812f9: Pulling fs layer 
151eb940bbec: Pulling fs layer 
0e9dda2495b9: Pulling fs layer 
0e78bdc2f297: Pulling fs layer 
8dc68d594a4e: Pulling fs layer 
dd2d5e8a2285: Pulling fs layer 
20aaffadccad: Pulling fs layer 
78c1b6a77f2a: Pulling fs layer 
3ceb5c165377: Pulling fs layer 
45e21824a7ba: Pulling fs layer 
8236d27657e2: Pulling fs layer 
5633157fc0be: Pulling fs layer 
92ac4d269791: Pulling fs layer 
40ce8bbe7afb: Pulling fs layer 
45ac43b06f56: Pulling fs layer 
8b9584b02d69: Pulling fs layer 
0d91c6dfa0c1: Pulling fs layer 
b9dc07c7c1ea: Pulling fs layer 
3d21f51710b4: Pulling fs layer 
6360bef962dd: Pulling fs layer 
f84c639be180: Pulling fs layer 
6ec5da232ee1: Pulling fs layer 
d7af86c56fa8: Pulling fs layer 
ba96052a8cc0: Pull complete 
2c6468ea0397: Pull complete 
0c385592fc6a: Pull complete 
656202f74c65: Pull complete 
ca047956c9db: Pull complete 
cb2e38bdd77d: Pull complete 
ca514b500ede: Pull complete 
301b1e807492: Pull complete 
7d1a4f244e1b: Pull complete 
3db8bbb5c53d: Pull complete 
146859387b0c: Pull complete 
8a6258e9e153: Pull complete 
c566da3518ef: Pull complete 

<b> 9. image classification  -  Thumbs Project  using ResNet

  https://learn.nvidia.com/courses/course?course_id=course-v1:DLI+S-RX-02+V2&unit=block-v1:DLI+S-RX-02+V2+type@vertical+block@aabe204272214ba69309581d388b0734

  <b> 10. image regression  -  Face XY Project

  https://learn.nvidia.com/courses/course?course_id=course-v1:DLI+S-RX-02+V2&unit=block-v1:DLI+S-RX-02+V2+type@vertical+block@76a2873eb69946b4928c4f8432e04314
