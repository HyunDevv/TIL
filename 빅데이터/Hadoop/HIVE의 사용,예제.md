# HIVE 예제

1. HIVE에 데이터 테이블 작성 및 파일 업로드
   

hive> CREATE TABLE HDI(id INT, country STRING, hdi FLOAT, lifeex INT, mysch INT, eysch INT, gni INT) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' STORED AS TEXTFILE;

- 하이브에서 테이블 작성 시 컬럼명에 한글이 들어가지 않도록 주의한다!



hive>load data local inpath '/root/hdi.txt' into table HDI;

- 로드할 데이터(csv)의 정제가 필요하다!
  - 윈도우에서 필요한 데이터 파일을 구한 후 `,`(콤마)로만 구분 되도록 정제한다
  - 인코딩 유형을 utf-8로 변경한다



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

   7) libfb303-X.jar                                 페이스북에서 제공

   8) log4j-X.jar

2. /usr/local/hadoop-1.2.1/hadoop-core-1.2.1.jar





java Program

![캡처](md-images/%EC%BA%A1%EC%B2%98.PNG)



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



LOAD DATA LOCAL INPATH '2008.csv' OVERWRITE INTO TABLE airline_delay PARTITION (delayYear='2008'); 





년도 별 출발 지연 시간, 도착 지연 기간의 평균을 구하시오

SELECT Year, avg(ArrDelay), avg(DepDelay) FROM airline_delay GROUP BY Year;



2008년도 별 출발 지연 시간, 도착 지연 기간의 평균을 구하시오

SELECT Year, avg(ArrDelay), avg(DepDelay) FROM airline_delay 

WHERE delayyear=2008

GROUP BY Year, Month

ORDER BY Year, Month;