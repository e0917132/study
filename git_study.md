## 1. **Git / GitHub**

#### 1-1. Git & GitHub를 사용해야하는 이유

- 파일이나 코드의 변경 이력을 체계적으로 기록/관리하기 위해서 사용한다.
- 협업, 백업, 추적성, 포트폴리오의 목적으로 사용한다.

#### 1-2. Git과 GitHub의 차이

- Git : 버전 관리를 위해 필요한 도구(프로그램) - 내 컴퓨터(로컬)에서 동작
- GitHub : Git 저장소를 올려두는 웹서비스 - 인터넷(원격)에서 동작

#### 1-3. Repository (저장소)

- 파일과 변경이력을 함께 관리하는 저장소.
    - 로컬 저장소: 내 컴퓨터에 있는 저장소. `git init`
    - 원격 저장소: GitHub 같은 서버에 있는 저장소. `git clone` (내 컴퓨터에 복사)

#### 1-4. Commit (커밋- 저장 시점)

- 변경 사항을 하나의 기록으로 저장하는 단위.
    - 각 커밋은 고유한 해시값(예:a38dnc)을 가진다.
    - 무엇을 왜 바꿨는지 메시지로 남긴다.
    - 되돌아 갈 수 있는 기준점 역할

#### 1-5. Branch (브랜치- 분기)

- 독립적으로 작업할 수 있는 공간
    - 원본(main)에 영향을 주지않고 기능 개발 가능
    - 여러 기능 동시 개발 가능
    - 작업이 끝나면 병합(merge) 함

#### 1-6. Head (헤드)

- 현재 내가 작업 중인 위치를 가리키는 포인터.

#### 1-7. Working Directory / Staging Area

- Working Directory : Git 에 기록되지 않은 변경사항이 있는 상태
- Staging Area : 다음 커밋에 포함할 변경사항을 미리 모아두는 공간

!(스크린샷 2026-10-08 오전 1.09.11.png)

## 2.  git 기본 명령어

- git config
    - Git의 기본 동작을 설정
    
    ```python
    # 전역 설정 (모든 저장소에 사용)
    git config --global user.name "홍길동"
    git config --global user.email "gildong@example.com"
    
    # 로컬 설정 (특정 저장소에만 사용)
    git config user.name "홍길동"
    git config user.email "gildong@example.com"
    ```
    
- git init
    - 현재 폴더를 Git 저장소(Repository)로 초기화
    - .git 폴더가 생성됨
- git status
    - 현재 Git 저장소의 상태를 확인
- git add
    - 변경된 파일을 Staging Area로 올리는 명령어
    - 커밋에 포함할 변경 사항을 선택하는 단계 → 커밋은 생성된 것 아님

```python
git add 파일명
```

- git commit
    - Staging Area에 있는 변경 사항을 하나의 버전으로 기록
    - 커밋 메시지 작성 규칙 : 명확하고 간결하게 작성 / 동사로 시작 / 한 커밋 = 한 작업

```python
git commit -m "커밋메시지"

# 커밋 이력 확인
git log

# 이력 전체 + 그래프
git log --all --graph
```

- git merge
    - 다른 브랜치의 작업 내용을 현재 브랜치로 합치는 명령어.

```python
git merge feat/이름
```

- git push
    - 로컬 저장소의 커밋을 원격 저장소(GitHub)에 업로드
    
    ```python
    # 원격 저장소 연결 (최초 1회)
    git remote add origin https://github.com/user/repo.git  
    
    # 최초 push: upstream 설정
    git push -u origin main    
    
    git push                   # 이후에는 이것만으로 충분
    ```
    
- git pull
    - 원격 저장소의 최신 변경 사항을 가져와 현재 브랜치에 합침
    
    ```python
    git pull origin main
    ```
    

**💡 .gitignore 파일**
- 버전 관리에서 제외할 파일을 지정하는 설정 파일
- 불필요한 파일(환경 변수 파일, 빌드 결과물, 개인 설정 파일 등)이 커밋되는 것을 방지
- 사용 방법: .gitignore 파일 생성 → 파일 안에 제외할 파일 이름 작성 → git add .gitignore → git commit -m “Add .gitignore”로 커밋하면 완료
- 이미 커밋되었을 경우는 추적목록에서 직접 빼줘야한다. 

## 3. **Branch**

#### 3-1. git branch 명령어

- git branch : 브랜치 목록 확인
- git branch feat/이름 : 브랜치 생성
- git switch feat/이름 : 브랜치 전환(위치 변경)

#### 3-2. 브랜치 관리(main, develop, feature, hotfix, release)

- main : 배포 가능한 안정 버전
- develop : 개발 중인 기능을 테스트하는 버전
- feature : 기능 개발
- hotfix : 긴급 수정
- release : 배포 준비. 배포 전 마무리 작업만 하는 공간

!(git_flow_branch_strategy_example.png)

#### 3-3. Fast-forward

- 병합하려는 브랜치가 직선으로 이어져 있을 때. 단순히 커밋 포인터만 이동.

!(fast_forward_merge_before_after.png)

#### 3-4. 3-way merge

- 두 브랜치가 각자 새로운 커밋을 가지고 갈라졌다가 다시 합쳐질 때. 병합 커밋이 생성된다.

!(three_way_merge_before_after.png)

#### 3-5. Merge conflict

- 3-way merge에서 두 브랜치가 같은 파일의 같은 부분을 서로 다르게 수정하면 충돌이 발생.
- 해결 방법
    - 충돌 파일 확인 → 충돌코드 직접 수정 → 새로운 커밋 생성