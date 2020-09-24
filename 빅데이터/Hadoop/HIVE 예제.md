# HIVE 예제

1. HIVE에 데이터 테이블 작성 및 파일 업로드



hive> CREATE TABLE HDI(id INT, country STRING, hdi FLOAT, lifeex INT, mysch INT, eysch INT, gni INT) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' STORED AS TEXTFILE;



hive>load data local inpath '/root/hdi.txt' into table HDI;



hive> select * from hdi limit 5;





2. Java Application 연동



hive 서버 실행 - Java 프로그램이 접속 할 수 있는 Deamon을 실행

[root]#hive --service hiveserver2



필요 라이브러리 (다운해서 이클립스 추가!!)

1. /usr/local/hive/lib에 있는 몇가지 jar

1) commons-logging-X.jar

2) hive-exec-X.jar

3) hive-jdbc-X.jar

4) hive-jdbc-X-standalone.jar

5) hive-metastore-X.jar

6) hive-service-X.jar

7) libfb303-X.jar

8) log4j-X.jar

2. /usr/local/hadoop-1.2.1/hadoop-core-1.2.1.jar





java Program



Class.forName("org.apache.hive.jdbc.HiveDriver");

Connection conn = DriverManager.getConnection



("jdbc:hive2://localhost:10000/default","root","111111");

Statement stmt = conn.createStatement();

ResultSet rs = stmt.executeQuery("SELECT * FROM HDI");

   while(rs.next()) {

​     System.out.println(rs.getString(1));

   }

conn.close();

System.out.println("Success....");





---



- air 데이터 예제



https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/HG7NV7 에서 다운



CREATE TABLE airline_delay(

Year INT,

MONTH INT,

DayofMonth INT,

DayofWeek INT,

DepTime INT,

CRSDepTime INT,

ArrTime INT,

CRSArrTime INT,

UniqueCarrier STRING,

FlightNum INT,

TailNum STRING,

ActualElapsedTime INT,

CRSElapsedTime INT,

AirTime INT,

ArrDelay INT,

DepDelay INT,

Origin STRING,

Dest STRING,

Distance INT,

TaxiIn INT,

TaxiOut INT,

Cancelled INT,

CancellationCode STRING

COMMENT 'A = carrier, B = weather, C = NAS, D = security',

Diverted INT COMMENT '1 = yes, 0 = no',

CarrierDelay STRING,

WeatherDelay STRING,

NASDelay STRING,

SecurityDelay STRING,

LateAircraftDelay STRING)

COMMENT 'TEST DATA'

PARTITIONED BY (delayYear INT)

ROW FORMAT DELIMITED

FIELDS TERMINATED BY ','

LINES TERMINATED BY '\n'

STORED AS TEXTFILE;



LOAD DATA LOCAL INPATH '2008.csv' OVERWRITE INTO TABLE airline_delay PARIRION (delayYear='2008'); 





년도 별 출발 지연 시간, 도착 지연 기간의 평균을 구하시오

SELECT Year, avg(ArrDelay), avg(DepDelay) FROM airline_delay GROUP BY Year;



2008년도 별 출발 지연 시간, 도착 지연 기간의 평균을 구하시오

SELECT Year, avg(ArrDelay), avg(DepDelay) FROM airline_delay 

WHERE delayyear=2008

GROUP BY Year, Month

ORDER BY Year, Month;