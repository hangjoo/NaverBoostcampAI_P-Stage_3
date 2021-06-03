# Hangjoo Codes

## How to train model.

이번 Competition Task에 맞는, 사용된 모델들은 config들은 custom_configs에 저장되어있습니다.

mmdet_train.py 혹은 mmdet_train.ipynb 코드 내에 model_cfg 부분에 custom_configs에 저장되어 있는 실행시키고자 하는 파일명을 넣은 뒤 실행시키면 학습이 진행됩니다.

이 외에 다른 추가 모델을 사용하고 싶으면 mmdet_get_config.ipynb를 사용하여 아래 코드와 같이 되어있는 셀 부분을 수정한 뒤 실행합니다.

```python
model_name = \
"detectors"

model_cfg = \
"DetectoRS_mstrain_400_1200_x101_32x4d_40e"

model_url = \
"https://www.cs.jhu.edu/~syqiao/DetectoRS/DetectoRS_X101-ed983634.pth"
```

configs/{model_name}/{model_cfg}.py로 저장되어있는 config 파일을 가져오며 model_url은 pretrained된 checkpoint 파일의 url입니다. mmdetection의 공식 깃헙 레포지토리에서 config 폴더 내에서 readme.md 파일에서 각 모델의 벤치마크 점수와 checkpoint 파일의 url을 확인할 수 있습니다.