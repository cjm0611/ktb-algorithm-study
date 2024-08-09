# ktb-algorithm-study
[본인의 Velog](https://velog.io/@cjm-0611/posts) 글에서 본문에 `[ktb-algorithm-study]` 키워드가 포함된 글을 자동으로 깃허브에 업로드합니다.
매일 자정(KST 기준)에 동작합니다.

<br />


## 코드 설명
```yml
name: Update Blog Posts ## GitHub Actions 인터페이스에 표시될 워크플로우 이름

  
on: # 워크플로우 트리거 방법 정의
  push:
      branches:
        - main  # 방법1 - main 브랜치에 커밋이 푸시될 때 실행
  schedule:
    - cron: '0 15 * * *'  # 방법 2 - 매일 자정에 실행 (UTC 15시, KST 00시)

jobs: # 워크 플로우에서 실행될 작업들
  update_blog: # 작업의 이름
    runs-on: ubuntu-latest # 작업이 실행될 환경 (최신 버전의 Ubuntu를 사용하는 가상 환경)

    steps: # 작업 내에서 수행할 각 단계
    - name: Checkout 
      uses: actions/checkout@v2 # GitHub 리포지토리의 코드를 가상 환경에 체크아웃

    - name: Push changes # 변경된 파일을 리포지토리에 커밋하고 푸시하는 단계
      run: |
        git config --global user.name 'github-actions[bot]'
        git config --global user.email 'github-actions[bot]@users.noreply.github.com'
        git push https://${{ secrets.GH_PAT }}@github.com/cjm0611/ktb-algorithm-study.git # 지정한 레포지터리에 푸쉬

    - name: Set up Python # Python 환경을 설정하는 단계
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'

    - name: Install dependencies # 파이썬 프로젝트에 필요한 의존성을 설치 (feedparser, gitpython)
      run: |
        pip install feedparser gitpython

    - name: Run script # 스크립트를 실행하는 단계
      run: python scripts/update_blog.py
```


<br />

## 참고 자료
https://velog.io/@rimgosu/velog-글-작성-시-자동으로-github에-커밋하기
