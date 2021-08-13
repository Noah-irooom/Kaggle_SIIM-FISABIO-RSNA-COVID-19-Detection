# 캐글 대회 : SIIM-FISABIO-RSNA-COVID-19-Detection
- Chest X-ray 이미지 Classification 및 Object Detection
- https://www.kaggle.com/c/siim-covid19-detection

## 1. 4class Classification

- 태스크 요약 : Chest X-ray 이미지를 4가지로 분류
  - Negative for Pneumonia
  - Typical Appearance
  - Indeterminate Appearance
  - Atypical Appearance

- 메소드 :
  - 1. .dcm to .png or .jpg
    - 의료영상은 dcm 확장자로 구성되어 있어 이를 .png 또는 .jpg로 바꾸는 과정 필요
  - 2. 이미지 어그멘테이션
    - random_flip
    - random_contrast
    - random_brightness
    - random_saturation 
  - 3. 큰 이미지와 큰 배치 사이즈가 성능이 더 나은 결과를 보임
  - 4. 모델 앙상블 적용
    - efficientnetb7
    - efficientnetv2 L (tfhub)
    - efficientnetv2 XL (tfhub)
    - resnetv2 152
    - resnet152
  - 5. 외부 xray 데이터셋 사용은 오히려 효과가 떨어짐.
    - 분류기준이 본 대회와 다르기 때문일 것으로 생각.


- validation mAP : 0.82 ~ 0.83


## 2. Object Detection

2.1. 2class Classification
- 태스크 요약 : Detection 전에 xray이미지에 opacity가 있는지 없는지 먼저 분류
  - none vs opacity(not none)

- 메소드 :
  - 1. 이미지 어그멘테이션
    - random_flip
    - random_contrast
    - random_brightness
    - random_saturation 
 
  - 2. 모델 앙상블 적용
    - efficientnetb7
    - resnetv2 152
    - resnet152

- validation mAP : 0.91

2.2. Object Detection
- 태스크 요약 : 환자 xray이미지 병변위치 detection
- 메소드 
  - 1. 이미지 어그멘테이션
    - Horizontal Flip
    - Vertical Flip
    - Image Crop
  - 2. 외부데이터셋 활용 
    - kaggle copmpetetion : RSNA pneumonia 
  - 3.사용 모델 
    - mmdetection faster rcnn pretrained (backbone res50)
    - mmdetection faster rcnn pretrained (backbone res101)
    - mmdetection cascade rcnn pretrained (backbone res101)
  - 4. detection 또한 앙상블 고민했다면 더 좋은 결과 나왔을 것으로 예상
    - detection 앙상블 API도 있음
      -  https://github.com/ZFTurbo/Weighted-Boxes-Fusion  참고

- validation mAP : 0.0.54 ~ 0.56 (Pascal평가 기준)

## 3. 총 점수
- 받은 점수 : Private 0.599, Public 0.611

## 4. 함께한 팀원
- 장두혁 https://github.com/justin95214
