# Complex YOLO(2018)

[GitHub - maudzung/Complex-YOLOv4-Pytorch: The PyTorch Implementation based on YOLOv4 of the paper: "Complex-YOLO: Real-time 3D Object Detection on Point Clouds"](https://github.com/maudzung/Complex-YOLOv4-Pytorch)

## Characteristic(Contributions)

![Untitled](Complex%20YOLO(2018)%20c3eeb8834fe34e4ebf71c7e0aa0715ac/Untitled.png)

- YOLO 알고리즘의 3D 버젼.
- BEV에서의 각도 예측이 어려웠던 점을 E-RPN method feature로 보완함.
- E-RPN method feature를(각도 값을 오일러 변환을 통해 imaginary part와 real part로 분할하여 인코딩한 값) 도입하여 BEV 이미지를 기반으로 객체의 각도 예측을 더 효율적으로 만듦.
- 다른 Lidar based 형태의 기법들과 달리 모든 class를 하나의 forward propagation path로 효율적으로 예측함.
- 높이 정보는 따로 예측하지 않기 때문에, 3D bbox 생성 시 사전에 각 object별로 입력된 높이를 사용함.
- YOLO 알고리즘에 E-RPN값만 추가한 형태이기 때문에 추후 개발된 YOLO알고리즘으로 대체와 성능 향상이 쉬울 것으로 보임.

## Model Structure

![Untitled](Complex%20YOLO(2018)%20c3eeb8834fe34e4ebf71c7e0aa0715ac/Untitled%201.png)

Complex YOLO모델의 BEV 데이터로는 point cloud 데이터의 height, intensity, density가 각각 R, G, B값에 대응되어 인코딩된다. 

Point cloud 범위는 본 논문에서는 ${x \in [0, 40m], y \in [-40m, 40m], z \in [-2m, 1.25m]}$ 로 제한한다. (트럭이 가장 높이가 큰 물체로 가정하여 3m가량의 높이로 잘라냄) 각도 예측을 위해 기존의 YOLO Grid에 Euler 변환된 각도의 imaginary, real값을 추가하여 E-RPN Grid를 생성한다. YOLOv2에서의 방식과 동일하게 각 Grid cell마다 5개의 객체(박스)를 예측한다.

## Loss Function

![Untitled](Complex%20YOLO(2018)%20c3eeb8834fe34e4ebf71c7e0aa0715ac/Untitled%202.png)

![Untitled](Complex%20YOLO(2018)%20c3eeb8834fe34e4ebf71c7e0aa0715ac/Untitled%203.png)

${L_{Yolo}}$ : YOLO loss(predefined)

$L_{Euler}$ : E-RPN loss

${\lambda_{coord}}$ : Scaling factor

${S}$ : Length of cell dimension

$B$ : Number of bboxes

$1^{obj}_{ij}$ : j th box in i th cell

$e^{ib_\phi}$ : Predicted phase

${e^{i\hat{b}_\phi}}$ : Target phase

$t_{im}$ : Predicted imaginary part

$t_{re}$ : Predicted real part

$\hat{t}_{im}$ : Target imaginary part

$\hat{t}_{re}$ : Target real part

## Model Performance

### Inference accuracy

- For KITTI validation set

![Untitled](Complex%20YOLO(2018)%20c3eeb8834fe34e4ebf71c7e0aa0715ac/Untitled%204.png)

![Untitled](Complex%20YOLO(2018)%20c3eeb8834fe34e4ebf71c7e0aa0715ac/Untitled%205.png)

### Inference speed

- For KITTI dataset with a Titan X GPU(6.70 TOPS(FP32), Tensor Cores None, CUDA Cores 3072) : 20ms