# 무식하게 풀기(brute force)
## 조건
* 총 경우의 수가 적을 때(입력의 크기가 작을 때)
## 시간복잡도 분석
* 총 경우의 수
## 완전 탐색 레시피
1. 최대 크기 입력을 가정했을 때 경우의 수를 계산하고 제한시간 내에 생성 가능할지 가늠
2. 답의 후보를 만드는 과정을 여러 개의 선택으로 분할
3. 그 중 한 조각을 선택해 답의 일부로 만들고 나머지 답을 재귀호출을 통해서 완성
4. 조각이 하나밖에 남지 않은 경우 기저사례로 선택해 처리

