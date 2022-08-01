---
title: "WSL2 Install & Setting"
categories:
- Development Settings
output:
 html_document:
   keep_md: true
date: '2022-07-27'
---

# WSL2(Windows Subsystem for Linux)

- windows 기능 켜기/끄기에서
![Untitled](/images/day07/WSL2/Untitled.png)

- windows 하이퍼바이저 플랫폼 체크 후 재부팅
- PC 정보에서 windows 버전정보 확인

![Untitled](/images/day07/WSL2/Untitled%201.png)

- powershell 관리자권한 실행 후 코드 실행

```python
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

```python
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

- 파일 다운로드 후 설치 후 실행

```python
https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
```

![Untitled](/images/day07/WSL2/Untitled%202.png)

- microsoft store 실행
- ubunto 20.04.4 LTS 다운

![Untitled](/images/day07/WSL2/Untitled%203.png)

- powershell에서 버전확인

```python
wsl -l -v
```

- powershell 관리자 실행 후 입력

```python
wsl --set-default-version 2
```

![Untitled](/images/day07/WSL2/Untitled%204.png)

- 버전이 1일때

![Untitled](/images/day07/WSL2/Untitled%205.png)

- 지우고 처음부터 진행

![Untitled](/images/day07/WSL2/Untitled%206.png)

### VSCode 와 WSL연결

- 시스템 환경 변수 변경에서 Path에서 VSCode 확인

![Untitled](/images/day07/WSL2/Untitled%207.png)

![Untitled](/images/day07/WSL2/Untitled%208.png)

![Untitled](/images/day07/WSL2/Untitled%209.png)

- VScode 확인
- 시스템에서도 확인 후 없으면 추가

![Untitled](/images/day07/WSL2/Untitled%2010.png)

- VScode에서 remote wsl설치

![Untitled](/images/day07/WSL2/Untitled%2011.png)

- VScode 재실행

![Untitled](/images/day07/WSL2/Untitled%2012.png)

- microsoft Store에서 windows terminal 다운
- ubuntu 실행

![Untitled](/images/day07/WSL2/Untitled%2013.png)

![Untitled](/images/day07/WSL2/Untitled%2014.png)

- 경로 home/human/airflow

```python
mkdir airflow
```

![Untitled](/images/day07/WSL2/Untitled%2015.png)

- 처음 진행 시

```python
sudo apt-get update
```

```python
sudo apt install python3-pip
```

- 가상환경 설정

```python
sudo pip3 install virtualenv
```

```python
virtualenv venv
```

```python
source venv/bin/activate
```

- 환경변수 설정

```python
vi ~/.bashrc
```

- i눌러서 편집모드로 진행

```python
export AIRFLOW_HOME=/경로
```

- 작성 후 esc후

```python
:wq!
```

- 시스템에 반영

```python
source ~/.bashrc
```

- 반영되었는지 확인

```python
echo $AIRFLOW_HOME
```

- 폴더지우는 명령어
    - 모든 폴더를 날린다

```python
rm -rf '파일/폴더명'
```