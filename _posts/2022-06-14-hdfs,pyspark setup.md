---
layout: post
title:  "하둡,스파크(PYSPARK) 로컬(mac) 환경 구성하기"
categories: infra
author: jwoo-o
---
* content
{:toc}

## STEP1. 하둡 설치
터미널에 명령 입력
```
brew install hadoop
```
만약 **brew**가 없다면 [Homebrew](https://brew.sh/index_ko)에 접속하여 설치해준다.

## STEP2. 환경변수 수정
```
cd /usr/local/Cellar/hadoop/3.3.2/libexec/etc/hadoop
vi hdfs-site.xml
```

```xml
<configuration xmlns:xi="http://www.w3.org/2001/XInclude">
	<property>
		<name>fs.defaultFS</name>
		<value>hdfs://localhost:8020</value>
	</property>
	<property>
		<name>dfs.namenode.name.dir</name>
		<value>file:///Users/we/app/data/namenode</value>
	</property>
	<property>
		<name>dfs.datanode.data.dir</name>
		<value>file:///Users/we/app/data/datanode</value>
	</property>
</configuration>
```

## STEP3. 하둡 실행
```
hdfs namenode -format
hdfs namenode &
hdfs datanode &
```

## STEP4. 파이썬, 스파크, 스칼라 설치
```
brew install apache-spark
brew install python3
brew install scala@2.12


pip3 install jupyter
```

## STEP5. 환경변수 설정
```
vi ~/.zshrc

## 스파크 버전 X.X.X는 본인이 설치한 버전으로 수정
export SPARK_HOME="/usr/local/Cellar/apache-spark/3.2.1/libexec"
export PATH=$PATH:$SPARK_HOME
export PYSPARK_PYTHON=python3
export PATH="/usr/local/opt/scala@2.12/bin:$PATH"
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS='notebook'
export PYTHONPATH=$SPARK_HOME/python/:$PYTHONPATH
export PYTHONPATH=$SPARK_HOME/python/lib/py4j-0.10.9.3-src.zip:$PYTHONPATH
```

## STEP6. PYSPARK 실행
```
pyspark
```
