# Naver Boostcamp AI Tech - P Stage 3

## 개요

### Semantic Segmentation & Object Detection

이미지 내에 존재하는 재활용 가능한 쓰레기를 분류하기 위해 재활용 가능한 쓰레기를 segmentation, detection하는 문제입니다.

전체 이미지는 총 4,109장으로 구성되어 있으며 이 중 2,617장이 학습에 사용될 이미지로, 655장이 검증에 사용될 이미지로, 나머지 837장 중 417이 Public Score를 계산할 이미지, 420장이 Private Score를 계산할 이미지로 구성되어 있습니다.

Semantic Segmentation과 Object Detection 두가지 task로 분리되어 있으며 각각 task에 대해서 점수를 따로 산출하는 방식입니다.

데이터 포맷은 coco annotation format으로 구성되어 있으며, 이미지는 (512, 512) 크기로 리사이징 되어 있습니다.

## 결과

### Semantic Segmentation

- Public Score : 0.6982 | Public Team Ranking : 4th
- Private Score : 0.6798 | Private Team Ranking : 5th

### Object Detection

- Public Score : 0.6074 | Public Team Ranking : 2nd
- Private Score : 0.4689 | Private Team Ranking : 9th

## 구현

### Semantic Segmentation

naive pytorch를 사용하여 학습 파이프라인을 구현했으며, [smp](https://github.com/qubvel/segmentation_models.pytorch) 라이브러리에서 구현된 pretrained 모델과 smp에 구현되지 않은 모델은 builder 디렉토리 내에 정의하여 사용했습니다.

P-Stage 2에서 HuggingFace 라이브러리가 Trainer 클래스를 이용하여 모델을 학습하는 것에 아이디어를 얻어, Trainer.py에 Trainer 클래스를 정의하여 학습시 Trainer 클래스 인스턴스에 적절한 인자를 넣어서 모델을 학습할 수 있도록 구현했습니다. 학습이 진행되는 과정을 단계별로 나눠 각각 클래스 메소드로 구현하여 가독성과 코드 수정 등의 유지 보수 시 편리하게 사용할 수 있었습니다.

학습에 사용될 파라미터나 어떤 모델을 사용할지 등의 config은 json 파일을 사용하여 관리하였으며, 추가적으로 neptune AI라는 실험관리 라이브러리를 추가로 사용하여 한눈에 여러 실험 결과를 비교할 수 있도록 구현했습니다.

### Object Detection

mmDetection 라이브러리를 사용하여 전체 파이프라인을 구현했으며, mmDetection 라이브러리 구현이 깔끔하게 잘 되어있어 필요한 부분이 생길 때마다 적절하게 내부 소스 코드를 조금씩 수정하면서 사용했습니다.

개인적으로 생각하는 mmDetection 라이브러리 장점은 폐쇄적이지 않고 많은 Object Detection 모델들이 mmDetection으로 구현되어 있는 경우가 많아서 좋은 성능을 보이는 Object Detection pretrained 모델을 쉽게 가져와 사용할 수 있었습니다.

mmDetection에서 제공하는 default config들이 coco-dataset 같은 범용적인 벤치마크를 위한 데이터셋에 맞춰서 설정되어 있기 때문에 p stage 3 competition에 맞춰 자동으로 적절하게 변환해주는 코드를 노트북 파일로 구현하여 사용했습니다.

## 회고

컴퓨터 비전 분야 중 대표적인 task인 semantic segmentation과 object detection을 직접 주어진 문제에 맞게 구현하고 해결할 수 있었던 좋은 경험이었습니다. 항상 객체 탐지 관련 모델과 이론을 공부하면서 이해가 잘 안되고 와닿지 않는 부분들이 많았는데 이번 컴피티션으로 많은 깨달음을 얻을 수 있었습니다.

특히 Object Detection은 컴퓨터 비전에서 가장 활발한 분야라고 생각될만큼 중요하다고 느끼기에 이번 경험이 더 값지다고 생각합니다. 아쉬웠던 점은 리더보드 점수가 public score에 눈이 멀어 public 리더보드 점수를 가중치로 사용하여 여러 모델을 앙상블 했던 것이 private 리더보드 점수 산출하면서 무너져버렸던 점이 아쉬웠습니다. 이걸로 후에 컴티피션에 참여할 때 주의해야할 좋은 교훈을 하나 또 얻었습니다.

평소 컴퓨터 비전 분야에 관심이 있었고 이 분야을 목표로 가지고 있던만큼 잠도 줄여가며 참 열심히 했던 컴피티션이었습니다.