---
title: "Apache Spark"
categories:
- Development Settings
output:
 html_document:
   keep_md: true
date: '2022-07-28'
---

### spark

- home/human에 hadoop폴더 만들기

```python
sudo apt-get install openjdk-8-jdk
```

- 코드를 실행하여 설치

```python
sudo wget https://archive.apache.org/dist/spark/spark-3.2.0/spark-3.2.0-bin-hadoop3.2.tgz
```

- 집 풀기

```python
sudo tar -xvzf spark-3.2.0-bin-hadoop3.2.tgz
```

### PySpark

- 자바 환경변수설정
    - vi ~/.bashrc에서

```python
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```

- PySpark 환경변수설정
    - vi ~/.bashrc에서

```python
export SPARK_HOME=spark3의 경로
export PATH=$SPARK_HOME/bin:$PATH
export PYSPARK_PYTHON=python3
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSAPRK_DRIVER_PYTHON_OPTS='notebook'
```

- 껐다 킨 후

```python
pyspark
```

- 가상환경을 들어간 후

```python
pip3 install findspark
pip3 install pyspark
pip3 install jupyter
```

- vi ~/.bashrc

```python
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSAPRK_DRIVER_PYTHON_OPTS='notebook'
```