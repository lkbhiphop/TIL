# Cloud9

개발할 컴퓨터 환경을 클라우드로 구축하는 서비스

계정기반이기때문에 어디서 접속하던지 똑같은 환경으로 개발 가능

#### linux 명령어

##### - 새로운 파일 생성하는 방법 touch

touch test.py

##### - python 버젼 확인

python -V / python3 -V

[pyenv] (url) 넣으면 하이퍼링크가능

##### - pip 리스트 확인

pip list



## pyenv 설치방법(내가 설정한 환경 전체에 파이썬 환경을 구축하는 방법)



- install

##### 1. github의 파일을 현재컴퓨터로 복사한다. = install

`git clone https://github.com/pyenv/pyenv.git ~/.pyenv`

##### 2. 환경변수 설정

밑에 3줄은 무슨의미인가요?

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile 

echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile

echo 'eval "$(pyenv init -)"' >> ~/.bash_profile

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
#echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
source ~/.bash_profile
# 환경변수 추가 후 bash_profile 실행 --> 터미널창 새로고침
```

##### 3. 파이썬 설치

```bashbash
pyenv install 3.6.1 # pyenv를 통해서 python 3.6.1실행
pyenv global 3.6.1 # 전역으로 버젼 설정
python -V # 파이썬 버젼 확인
pyevn versions # 사용가능한 파이썬 버젼 리스트 출력


```

## pyenv virtualenv(global이 아닌 특정 환경에 가상환경 구축)

##### 1. github의 파일을 현재컴퓨터로 복사한다. = install

```bash
git clone https://github.com/pyenv/pyenv-virtualenv.git $PYENV_ROOT/plugins/pyenv-virtualenv
```

##### 2. 환경변수 설정

왜 위에 3가지 과정은 하지 않나요?

```bash
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profileb
source ~/.bash_profile
```

##### 3. 가상환경 실제로 만들기 - pyenv virtaulenv <파이썬버젼> <가상환경이름>

```bash
pyenv virtual 3.6.1 confi
```

##### 4. 글로벌 --> 가상파이썬환경 bash로 가기

```bash
pyenv shell confi
```



