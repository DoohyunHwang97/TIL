# git-flow
![git-flow-image](https://devocean.sk.com/editorImg/2024/8/21/6e8114c0510c505512467f476426cc89303e0de5cdd5dc1c9e95d6e3bc538f62)
## 브랜치별 역할
### 1. main
* 사용자에게 서비스될 브랜치
* 버그 발생시 hotfix 브랜치 생성 후 merge
### 2. hotfix
* main에서 버그가 있을 경우 생성되는 임시 브랜치
* 버그가 해결되면 main, develop에 merge 후 삭제된다
### 3. release
* 다음 버전 출시를 대비하는 브랜치
* develop에서 qa를 위해서 만드는 임시 브랜치
* test를 거친 후 변경사항은 develop으로 merge 되고 main 브랜치로 병합한다
### 4. develop
* 다음 출시 버전 대비하여 개발하는 브랜치
### 5. feature
* 새로운 기능을 개발하는 불안정한 브랜치
* develop에 병합하기 전에 test가 필요하다

## work-flow
### 1. 신규 기능 개발
* feature 브랜치를 새로 생성후 신규 기능 개발
* develop 브랜치에 병합
### 2. 다음 버전 출시
* develop 브랜치에서 release 브랜치 생성
* qa 및 테스트 후 main 브랜치에 병합
### 3. main 버그 수정
* main에서 버그 발생시 hotfix 브랜치 생성
* hotfix 브랜치 변경 사항 main, develop 에 모두 반영
## 참고 자료
[브랜치 전략](https://inpa.tistory.com/entry/GIT-%E2%9A%A1%EF%B8%8F-github-flow-git-flow-%F0%9F%93%88-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EC%A0%84%EB%9E%B5)