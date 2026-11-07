Cantilever Beam Resonance Avoidance & Bending Moment Optimization

Overview

본 프로젝트는 외팔보에 부착된 두 질량체의 위치를 최적화하여 1차 및 2차 고유진동수의 지정된 공진 회피 조건을 만족하면서, 고정단에 발생하는 추가 굽힘모멘트를 최소화하는 알고리즘을 구현한 것입니다.

오일러–베르누이 보 이론(Euler–Bernoulli Beam Theory)과 유한요소법(Finite Element Method, FEM)을 이용하여 질량체의 배치에 따른 고유진동수를 예측하고, 가능한 배치를 탐색하여 최적의 질량 배치를 선정합니다.

Algorithm

알고리즘은 다음 순서로 진행됩니다.

고유진동수 예측: 3차 에르미트 보간함수를 이용한 유한요소 모델을 구성하고, 두 집중질량의 위치에 따른 1차 및 2차 고유진동수를 계산합니다.

후보 배치 생성: 지정된 위치 범위와 탐색 간격에 따라 가능한 두 질량체의 배치 조합을 생성합니다.

공진 회피 조건 판별: 두 고유진동수가 각각 지정된 회피 범위를 벗어나는 배치만 선별합니다.

굽힘모멘트 최소화: 선별된 배치 중 고정단의 추가 굽힘모멘트가 최소인 배치를 선정합니다.

최종 배치 선정: 최소 굽힘모멘트가 동일한 배치가 여러 개라면 공진 회피 여유 거리가 가장 큰 배치를 선정합니다.

추가 굽힘모멘트는 다음 식으로 계산합니다.

T = mg(2L − a − b)

L: 외팔보의 길이

m: 각 질량체의 질량

g: 중력가속도

a, b: 자유단으로부터 측정한 두 질량체의 부착 위치

Experimental Validation

개발한 알고리즘은 두 가지 외팔보 조건을 이용하여 검토하였습니다.

1. Numerical Model Validation

외팔보 길이: 30 cm

질량체: 99 g × 2

검증 배치: 45개

평가 방법: 예측 고유진동수와 FFT 실측값 비교

2. Algorithm Validation

외팔보 길이: 15 cm

질량체: 50 g × 2

전체 후보 배치: 78개

공진 회피 조건을 만족하는 배치: 30개

선정된 최적 배치: (7, 12) cm

최소 추가 굽힘모멘트: 0.05396 N·m

선정한 최적 배치에서 1차 및 2차 고유진동수가 모두 지정된 공진 회피 범위를 벗어남을 실험적으로 확인하였습니다.

다섯 가지 검증 배치에서의 평균 절대백분율오차는 1차 고유진동수 약 1.41%, 2차 고유진동수 약 0.72%였으며, 공진 회피 판정은 모두 실측 결과와 일치하였습니다.

또한 최적 배치의 추가 굽힘모멘트는 공진 회피 조건을 만족하는 배치의 평균 대비 약 31.25%, 최댓값 대비 약 50.00% 감소하였습니다.

Installation & Usage

Requirements: Python 3.10 이상

의존성 설치:

python -m pip install -r requirements.txt

15 cm 외팔보 최적화 실행:

python main.py --preset 15cm

30 cm 외팔보 최적화 실행:

python main.py --preset 30cm-1cm

복수 최적해 선정 사례 실행:

python main.py --preset 30cm-tie

실험값과 예측값 비교:

python validate_report.py

전체 후보 배치 결과를 CSV로 저장하려면 --csv 옵션을 추가합니다.

예시:

python main.py --preset 15cm --csv results/15cm_candidates.csv

Project Structure

beam_optimizer.py — 유한요소 해석 및 최적 배치 선정 알고리즘

main.py — 알고리즘 실행 및 결과 저장

validate_report.py — 수치해석 결과와 실측값 비교

examples/ — 외팔보 조건별 입력 설정

data/ — 실험 측정 데이터

tests/ — 알고리즘 자동 검증 코드

requirements.txt — Python 의존성

Limitations

본 연구에서는 선형 탄성 및 작은 변형을 가정한 오일러–베르누이 보 모델을 사용하였습니다. 집중질량의 회전관성, 부착에 따른 강성 변화 및 감쇠 효과는 수치해석 모델에서 고려하지 않았습니다.
