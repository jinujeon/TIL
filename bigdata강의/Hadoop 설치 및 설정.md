#  Hadoop 설치 및 설정

1. 리눅스 서버를 준비한다

   +hostname 설정

   - hostnamectl set-hostname server1

   \- vi /etc/hosts

   192.168.111.101 server1

   +ip 설정 
       cd /etc/sysconfig/network-scripts/

   -> vi ifcfg-ens33-> IPADDR 변경 
   -> systemctl restart network 
   -> ifconfig로 확인

2. 자바를 설치한다

3. 하둡 설치

   > 네트워크 상의 다른 컴퓨터에 로그인하거나 원격 시스템에서 명령을 실행하고, 다른 시스템으로 파일을 복사할 수 있게 해주는 응용 프로토콜. 암호화 기법을 사용한다

   0.  Firewall stop

      \- systemctl stop firewalld

      \- systemctl disable firewalld

   1. 보안 설정 (public, pirvate key를 생성)
      - dsa는 암호화 방식
      - 자기컴으로 들어갈 때도 필요

      ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa

      cd

      cd .ssh (.ssh에 가서)

      키 전송

      cat id_dsa.pub >> authorized_keys (자신에게 만들 때, 가상분산모드 일 때)

      ​	[root@server .ssh]# ls
      ​    authorized_keys  id_dsa  id_dsa.pub 
      ​ssh-copy-id -i /root/.ssh/id_dsa.pub root@secondserver (secondserver에 키를 줄 때, 완전분산모드 일 때)

      ssh hadoopserver (확인 후 exit)

      ​	1.1 보안설정이 완료되면 파일을 전송할 수 있다!! (파일만가능! 폴더안됨!)

      ​	ex) scp /etc/hosts root@secondserver:/etc/hosts [scp 파일이름 루트권한으로 어디서버에 어디로 	복사]

      ​	1.2 다른 컴퓨터로 가서 명령 실행 가능

      ​	ex) ssh root@dataserver cp -r  /root/jdk1.8.0 /usr/local

      필요한 파일들을 전송한다. (jdk, java, /etc/profile, (하둡설치 이후에 - 하둡, 설정이후에 - 하둡설정폴더묶음파일))

      필요한 명령들을 실행한다. (jdk압축풀기, 이름변경, 복사)

   2. hadoop 설치

      wget https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz

      tar xvf hadoop-1.2.1.tar.gz 

      cp -r hadoop-1.2.1 /usr/local

      vi /etc/profile

      HADOOP_HOME 지정 (52줄)(순서 안 바뀌게 조심!)

      ```bash
      JAVA_HOME=/usr/local/jdk1.8.0
      CLASSPATH=/usr/local/jdk1.8.0/lib
      HADOOP_HOME=/usr/local/hadoop-1.2.1
      export JAVA_HOME  CLASSPATH HADOOP_HOME
      PATH=$JAVA_HOME/bin:$HADOOP_HOME/bin:.:$PATH
      ```

      후에 **reboot!!!**

      

   3. 환경설정 파일 수정

      

      cd /usr/local/hadoop-1.2.1/conf에서!!

      

      vi core-site.xml

      <configuration>

      <property>

      <name>fs.default.name</name>

      <value>hdfs://localhost:9000</value>  #localhost에는 메인컴퓨터 이름 ex)mainserver

      </property>

      <property>

      <name>hadoop.tmp.dir</name>

      <value>/usr/local/hadoop-1.2.1/tmp</value>

      </property>

      </configuration>

      

      vi hdfs-site.xml

      <configuration>

      <property>

      <name>dfs.replication</name>

      <value>1</value>     #복제되는 숫자!!

      </property>

      <property>

      <name>dfs.webhdfs.enabled</name>

      <value>true</value>

      </property>

      <property>

      <name>dfs.name.dir</name>

      <value>/usr/local/hadoop-1.2.1/name</value>

      </property>

      <property>

      <name>dfs.data.dir</name>

      <value>/usr/local/hadoop-1.2.1/data</value>

      </property>

      </configuration>

      

      vi mapred-site.xml

      <configuration>

      <property>

      <name>mapred.job.tracker</name>

      <value>localhost:9001</value>    #localhost에는 메인컴퓨터 이름 ex)mainserver   (데이터노드에서 작업한 내용을 메인서버로 전송해라)

      </property>

      </configuration>

      

      vi hadoop-env.sh

      9 export JAVA_HOME=/usr/local/jdk1.8.0

      10 export HADOOP_HOME_WARN_SUPPRESS="TRUE"

      

      vi slaves 

      localhost

      

      (완전분산모드 시)

      vi masters             #보조네임노드를 실행할 서버 설정 
   
      secondserver
      
      
      
      vi slaves                #데이터노드를 실행할 서버 설정
      
      dataserver
      
      
      
      /usr/local에서 tar cvfz hadoop.tar.gz ./hadoop-1.2.1
      
      scp hadoop.tar.gz root@secondserver:/usr/local
      
      ssh root@secondserver tar xvf /usr/local/hadoop.tar.gz 했는데 루트에 풀려서 이동 
      
      ssh root@secondserver mv /root/hadoop-1.2.1 /usr/local



   4. Hadoop 실행

      hadoop namenode -format 하면 name 폴더가 만들어진다

      start-all.sh

      jps

      

      firefox에서 http://서버이름:50070 로 확인

      

---



- 초기화 하려면?
0. stop-all.sh
  
1. /usr/local/hadoop-1.2.1/name, data, tmp 삭제
  2. .ssh에 있는 키값 삭제



- 리눅스 끌 때

  stop-all.sh 하고 끈다
  
  



- 완전 분산 모드 예제
  firefox에서 분석용 데이터 다운
  https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/HG7NV7

  hadoop fs -mkdir /air

  hadoop fs -put 2007.csv   /air

  cd /usr/local/hadoop-1.2.1
  hadoop jar hadoop-examples-1.2.1.jar  wordcount  /air  /output



- 맵리듀스 java파일 보기

  하둡 디렉토리에서 
  cd src

  cd examples

  cd org

  cd apache

  cd hadoop

  cd examples

  vi wordcount.java