# kaggle study

## animal object detection
<br>

### Dataset
- 1204장 train data, 300장 test data (image)
- train, test 객체의 bbox 좌표
- 4개 class - zebra, elephant, rhino, buffalo

<br><br>

## scoring
<br>
map@75

<br><br>

## Code
<br>

### Data
- 데이터 다운 받은 후 YOLO 형식의 폴더 구조로 재구성
- YOLO 학습에 필요한 annotation 파일 생성
- YOLO 학습에 필요한 yaml 파일 생성
- train test split

<br>

### model
train.py 코드와 학습 결과를 보면, YOLOv5에서 기본적으로 제공해주는 스코어는 map50과 map50-95(5단위)입니다.  제가 필요했던 스코어는 map75였기 때문에 val.py를 수정하여 map75를 얻어야 했습니다. 이를 위해 val.py에 구현되어 있던 map50 구현 코드를 map75로 출력되게 수정하였습니다. 밑에 과정을 적어 두었습니다.

- val.py에서 ap50을 포함한 변수(map50, ap50), 총 11개를 map50 -> map75, ap50 -> ap75 로 변경
- 277L 에서 ap[:, 0] -> ap[:, 5] 로 변경하여 50~95를 10등분한 것에서 5번째인 ap75를 가져옴

train과 test의 결과는 yolov5/runs에서 확인할 수 있습니다

<br><br><br>

### reference
https://github.com/ultralytics/yolov5
