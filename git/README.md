# 🌟 Git-Flow 브랜치 전략

## 📘 Git-Flow란?
Git-Flow는 Vincent Driessen이 제안한 Git 사용을 위한 브랜치 관리 전략입니다. 복잡한 프로젝트 관리를 위해 개발, 릴리스, 유지보수를 체계적으로 할 수 있게 돕습니다.

## 🌲 브랜치 종류
- **Master**: 항상 안정적인 상태로, 프로덕션 레벨의 준비가 완료된 코드만을 포함합니다.
- **Develop**: 다음 릴리스를 준비하는 개발 작업이 이루어지는 브랜치입니다.
- **Feature**: 새로운 기능 개발을 위한 브랜치. 개발 완료 후 Develop 브랜치로 병합합니다.
- **Release**: 릴리스 전 버그 수정, 문서 작업 등 마무리 작업을 위한 브랜치. 작업 완료 후 Master와 Develop에 병합됩니다.
- **Hotfix**: 프로덕션 릴리스에서 발생한 버그를 긴급하게 수정하기 위한 브랜치. 수정 후 Master와 Develop에 병합됩니다.

## 🔄 Git-Flow 사용 예시
이 예시에서는 새로운 로그인 기능을 추가하는 과정을 통해 Git-Flow 전략을 적용하는 방법을 설명합니다.

### 1. **새 기능 개발을 위한 Feature 브랜치 생성**
   - **목적**: 새로운 로그인 기능 개발
   - **브랜치 생성 및 이동**:
     ```
     git checkout develop
     git checkout -b feature/login-feature
     ```
   - **개발 시작**: 로그인 관련 코드 작성 및 테스트 진행

### 2. **개발 완료 후 Develop에 병합**
   - **목적**: 개발된 기능을 메인 개발 라인에 통합
   - **병합 작업**:
     ```
     git checkout develop
     git merge --no-ff feature/login-feature
     ```
   - **Feature 브랜치 삭제**:
     ```
     git branch -d feature/login-feature
     ```

### 3. **릴리스 준비**
   - **목적**: 다음 버전 릴리스 준비
   - **릴리스 브랜치 생성 및 버전 번호 지정**:
     ```
     git checkout -b release/1.2.0 develop
     ```
   - **릴리스 전 최종 테스트 및 버그 수정**

### 4. **릴리스 후 Master에 병합 및 태그 추가**
   - **목적**: 안정적인 릴리스를 프로덕션에 배포
   - **Master 브랜치에 릴리스 병합 및 버전 태깅**:
     ```
     git checkout master
     git merge --no-ff release/1.2.0
     git tag -a v1.2.0
     ```

### 5. **핫픽스 작업**
   - **목적**: 프로덕션에서 발생한 긴급 버그 수정
   - **핫픽스 브랜치 생성 및 수정 작업**:
     ```
     git checkout -b hotfix/urgent-login-fix master
     ```
   - **핫픽스 테스트 후 Master와 Develop에 병합 및 태그 추가**:
     ```
     git checkout master
     git merge --no-ff hotfix/urgent-login-fix
     git tag -a v1.2.1
     git checkout develop
     git merge --no-ff hotfix/urgent-login-fix
     ```

## 📊 장단점
### 장점
- **구조화된 접근**: 브랜치의 역할이 명확하여 대규모 팀과 프로젝트에 적합합니다.
- **분명한 릴리스 사이클**: 릴리스 준비, 개발, 유지보수가 체계적으로 이루어집니다.
- **긴급 수정 용이**: 핫픽스 브랜치를 통해 신속한 버그 수정이 가능합니다.

### 단점
- **복잡성**: 작은 팀이나 간단한 프로젝트에는 오버헤드가 될 수 있습니다.
- **학습 곡선**: Git-Flow 전략을 처음 접하는 사용자에게 다소 복잡하게 느껴질 수 있습니다.
