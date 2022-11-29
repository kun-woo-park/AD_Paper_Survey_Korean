# SEE-MTDA(2021, IEEE RA-L 2022)

[GitHub - darrenjkt/SEE-MTDA: (RA-L 2022) See Eye to Eye: A Lidar-Agnostic 3D Detection Framework for Unsupervised Multi-Target Domain Adaptation.](https://github.com/darrenjkt/SEE-MTDA)

## Characteristic(Contributions)

![Untitled](SEE-MTDA(2021,%20IEEE%20RA-L%202022)%203f2eaf51629e426dafd07ad7f0b2616c/Untitled.png)

- Lidar 데이터의 경우 데이터 셋 간 lidar 스캔 방식이 다르기 때문에 분포의 차이가 발생함
- 특정 lidar의 경우 스캔 방식이 조절 가능한 경우도 있는데, 이런 경우들에 대해 매번 fine tuning을 해주는 것은 비효율적임
- 따라서 lidar의 스캔 방식에 상관없이 perception model이 적용 가능한 preprocessing 알고리즘을 개발함
- 어떠한 perception model에도 적용 가능함

## Methods and Materials

- Object isolation
    - 학습 시에 ground truth 정보를 기반으로 object들을 구분해둠
    - 추론 시에는 카메라 정보를 기반으로 2d object의 위치 부근의 point들을 따로 object로 구분해둠
- Mesh interpolation
    - Ball-pivoting algorithm 기반으로 추출된 object의 point들을 mesh형태로 interpolation함
- Sampling points
    - Possion disk sampling을 통해 interpolated된 mesh에서 point들을 추출함