# 1. 트랜잭션이란 무엇인지 설명해주시고 트랜잭션의 특성을 말씀해주세요.

### [답변]

트랜잭션이란 단일한 논리적인 작업 단위로 트랜잭션 내의 작업들 모두가 성공적으로 시행되었을 때만 DB에 반영됩니다.


    💡 둘 이상의 SQL문(SQL 묶음)이 성공해야지만 의미가 있는 작업(ex: 계좌 이체)
    
    데이터베이스의 상태를 변화시키는 일의 단위입니다.
    
    단일한 논리적인 작업 단위
    
    논리적인 이유로 여러 SQL문들을 단일 작업으로 묶어서 나눠질 수 없게 만든 것
    
    트랜잭션의 SQL문들 중에 일부만 성공해서 DB에 반영되는 일은 일어나지 않는다.
    
    특징: ACID



**트랜잭션에서 commit**

지금까지 작업한 내용을 DB에 영구적으로 저장, 트랜잭션 종료


**트랜잭션에서 rollback**

지금까지 작업들을 취소하고(현 트랜잭션) 트랜잭션 이전 상태로 되돌린다. 트랜잭션 종료


**auto commit**

각각 sql문을 자동으로 트랜잭션 처리 해줌 → 성공하면 커밋 아니면 롤백

트랜잭션을 시작하면 auto commit은 비활성화됨


**트랜잭션 상태**

활동(Active): 트랜잭션이 실행중인 상태

실패(Failed): ****트랜잭션 실행에 오류가 발생하여 중단된 상태

철회(Aborted): 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태

부분 완료(Partially Committed): 트랜잭션의 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태

완료(Committed): ****트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태


**[나의 경험]**

Transactional으로 인한 영속성 반영 지연

스프링 @Transactional 은 메소드가 성공적으로 return 하게 되면 commit이 이루어져서

해당 데이터를 db에서 조회가 안되는 상황 발생

SimpleJpaRepository의 save() 메소드는 @Transactional 포함


# 2. OLTP와 OLAP의 차이점이 무엇인가요?

### [답변]

OLAP와 OLTP의 차이점으론 사용 목적의  차이가 있습니다. OLAP는 데이터를 다차원으로 분석할 수 있도록 도와주는 결정 지원 시스템이고, OLTP는 트랜잭션 지향 애플리케이션을 손쉽게 관리할 수 있도록 도와주는 정보 시스템입니다.

그래서 OLAP는 주로 데이터 조회에 자주 쓰이고, OLTP는 갱신에 주로 쓰인다고 알고 있습니다.

**OLAP(온라인 분석 처리)**

사용자가 동일한 데이터를 가지고 여러 기준으로, 다차원 데이터 분석을 할 수 있도록 도와주는 의사결정 지원 시스템

정보 위주의 분석처리로 쉽고 빠르게 다차원적인 데이터 접근으로 의사결정에 활용하는 기술

데이터 조회가 목적

**OLTP(온라인 트랜잭션 처리)**

트랜잭션 지향 애플리케이션을 손쉽게 관리할 수 있도록 도와주는 정보 시스템

여러 단말에서 보내온 메세지에 따라 호스트 컴퓨터가 데이터베이스를 액세스하고 바로 처리하는 형태

실시간으로 데이터베이스의 데이터를 갱신 또는 검색하는 작업을 처리하는 방식

데이터 갱신이 목적


|  | OLTP | OLAP |
| --- | --- | --- |
| 데이터 구조 | 복잡 | 단순 |
| 데이터 갱신 | 동적으로 순간적 | 정적으로 주기적 |
| 데이터 특성 | 트랜잭션 중심 | 주제 중심 |
| 데이터 크기 | 수 기가 바이트 | 수 테라 바이트 |
| 데이터 특성 | 정규화 X | 정규화 O |

| 기준 | OLAP | OLTP |
| --- | --- | --- |
| 용도 | OLAP는 대량의 데이터를 분석하여 의사 결정을 지원하는 데 도움이 됩니다. | OLTP는 실시간 트랜잭션을 관리하고 처리하는 데 도움이 됩니다. |
| 데이터 소스 | OLAP는 여러 소스의 기록 및 집계 데이터를 사용합니다. | OLTP는 단일 소스의 실시간 및 트랜잭션 데이터를 사용합니다. |
| 데이터 구조 | OLAP는 다차원(큐브) 또는 관계형 데이터베이스를 사용합니다. | OLTP는 관계형 데이터베이스를 사용합니다. |
| 데이터 모델 | OLAP는 별 스키마, 눈송이 스키마 또는 기타 분석 모델을 사용합니다. | OLTP는 정규화되거나 비정규화된 모델을 사용합니다. |
| 데이터 볼륨 | OLAP에는 대용량 스토리지가 필요합니다. 테라바이트(TB)와 페타바이트(PB) 규모라고 생각할 수 있습니다. | OLTP는 스토리지 요구 사항이 비교적 작습니다. 기가바이트(GB) 규모라고 생각하면 됩니다. |
| 응답 시간 | OLAP의 응답 시간은 일반적으로 초 또는 분 단위로 더 깁니다. | OLTP는 응답 시간이 짧으며 일반적으로 밀리초 단위입니다. |
| 예제 애플리케이션 | OLAP는 추세를 분석하고, 고객 행동을 예측하며, 수익성을 식별하는 데 유용합니다. | OLTP는 결제 처리, 고객 데이터 관리 및 주문 처리에 적합합니다. |

| 구분 | OLTP | OLAP |
| --- | --- | --- |
| 목적 | 비즈니스 활동 지원 | 비즈니스 활동에 대한 평가,분석 |
| 주 트랜잭션 형태 | SELECT, INSERT, UPDATE, DELETE | SELECT |
| 속도 | 수초 이내 | 수초 이상 수분 이내 |
| 데이터 표현 시간 | 실시간 | 과거 |
| 관리단위 | 테이블 | 분석된 정보 |
| 최적화 방법 | 트랜잭션 효율화, 무결성의 극대화 | 조회 속도, 정보의 가치, 편의성 |
| 데이터의 특성 | 트랜잭션 중심 | 정보 중심 |
| 예시 | 회원정보 수정 | 1년간의 주요 인기 트랜드 |
|  | 상품주문 | 한달간의 항목별 수입, 지출 |
|  | 댓글 남기기 및 수정 | 10년간 A회사의 직급별 임금 상승률 |


# 3. 인덱스의 개념, 장점, 종류에 대해서 설명해주세요.

### [답변]

**인덱스**는 테이블의 검색 속도를 향상시키기 위한
컬럼의 값과 물리적 주소를 (key, value)의 한 쌍으로 저장하는 자료구조입니다.

**장점**은 사용 목적처럼 빠른 데이터 조회가 가능하다는 점 입니다.

**종류**로는 B-(+)Tree, Hash Tree, Multicolumn index가 있습니다.

**종류**

B-Tree: O(logN)

B+Tree: B-와 달리 leaf tree에만 값 존재

multicolumn index: 두 가지 이상의 애트리뷰트를 인덱스로 만들때 사용

covering index: 조회하는 애트리뷰트들이 인덱스안에 존재한다면 테이블에 가지않고도 조회가 가능하여 조회 속도가 빠름

hash index: O(1), equality 비교만 가능

**full scan(table scan) → O(n)이 유리한 경우**

- 데이터가 조금 있는 경우
- 조회하려는 데이터가 테이블의 상당 부분 차지할 때

**인덱스 사용이 유리한 경우**

- 규모가 큰 테이블
- 삽입(INSERT), 수정(UPDATE), 삭제(DELETE) 작업이 자주 발생하지 않는 컬럼
- WHERE나 ORDER BY, JOIN 등이 자주 사용되는 컬럼
- 데이터의 중복도가 낮은 컬럼

**Index를 쓰는 이유**

- 조건을 만족하는 튜플을 빠르게 조회하기 위해
- 빠르게 정렬(Order by)하거나 그룹핑(Group by) 하기 위해

**인덱스 생성**

INDEX () ON { ()}

primary key에는 index가 자동 생성된다.(mysql 같은 경우에는 foreign key도)

**주의 사항**

사용되는 쿼리에 맞춰서 적절하게 index를 걸어줘야 쿼리가 빠르게 처리될 수 있다.

table에 write할때마다 index 변경 발생, 추가적인 저장 공간 차지 ⇒ 불필요한 인덱스 생성 X

explain → 사용될 수 있는 인덱스랑 사용된 인덱스가 출력

optimizer가 자동 선택

use index → 내가 선택 권유

force index → use보다 조금 강제

ignore index → 이건 제외

# 4. 사용해보신 데이터베이스 중 하나를 골라 해당 데이터베이스의 엔진이 무엇이었는지, 해당 엔진의 특징은 무엇인지 설명해주세요.

### [답변]

MySQL을 사용해보았구, SQL에는 **InnoDB, MyISAM, Archive** 등 8개의 엔진이 존재하는 걸로 알고 있습니다.

- **InnoDB** : 따로 스토리지 엔진을 명시하지 않으면 default 로 설정되는 스토리지 엔진이다. InnoDB는 transaction-safe 하며, 커밋과 롤백, 그리고 데이터 복구 기능을 제공하므로 데이터를 효과적으로 보호 할 수 있다.InnoDB는 기본적으로 row-level locking 제공하며, 또한 데이터를 clustered index에 저장하여 PK 기반의 query의 I/O 비용을 줄인다. 또한 FK 제약을 제공하여 데이터 무결성을 보장한다.
- **MyISAM** : 트랜잭션을 지원하지 않고 table-level locking을 제공한다. 따라서 multi-thread 환경에서 성능이 저하 될 수 있다. 특정 세션이 테이블을 변경하는 동안 테이블 단위로 lock이 잡히기 때문이다.텍스트 전문 검색(Fulltext Searching)과 지리정보 처리 기능도 지원되는데, 이를 사용할 시에는 파티셔닝을 사용할 수 없다는 단점이 있다.
- **Archive** : '로그 수집'에 적합한 엔진이다. 데이터가 메모리상에서 압축되고 압축된 상태로 디스크에 저장이 되기 때문에 row-level locking이 가능하다.다만,. 따라서 거의 가공하지 않을 원시 로그 데이터를 관리하는데에 효율적일 수 있고, 테이블 파티셔닝도 지원한다. 다만 트랜잭션은 지원하지 않는다. 한번 INSERT된 데이터는 UPDATE, DELETE를 사용할 수 없으며 인덱스를 지원하지 않는다

# 5. 정규화와 비정규화에 대해 설명해주세요.

### [답변]

**정규화**는 관계형 데이터베이스에서
데이터 모델의 중복을 최소화하고 데이터의 일관성, 유연성을 확보하기 위한 목적으로
데이터를 분해하는 과정입니다.

반면 **비정규화**는 시스템의 성능 향상, 개발 및 운영의 편의성 등을 위해 정규화 과정을 거치지 않는 행위입니다.

**DB 정규화**

데이터 중복과 insertion, update, deletion anomaly를 최소화하기 위해 일련의 NF(normal forms)에 따라 relational DB를 구성하는 과정

**NF(normal forms)**

![](./image/NF.png)

1NF ~ BCNF: FD와 key만으로 정의됨

1NF: 애트리뷰트의 value는 반드시 나워질 수 없는 단일한 값이어야 한다.(원자성)

2NF: 모든 non-prime 애트리뷰트는 모든 key에 fully FD해야 한다.

3NF: 모든 non-prime 애트리뷰트는 어떤 key에도 transitive FD(x→y & y→z , x→z) 하면 안된다.(non-prime와 non-prime 사이에는 FD가 있으면 안된다.)

BCNF: 모든 유효한 non-trivial FD(y가 x의 부분집합이 아니면) x→y는 x가 super key여야 한다.

FD(functionally dependent)

어떤 테이블 R에 존재하는 필드들의 부분집합을 각각 X와 Y라고 할 때, X의 한 값이 Y에 속한 오직 하나의 값에만 사상될 경우에 "Y는 X에 함수 종속 (Y is functionally dependent on X)"이라고 하며, X→Y라고 표기한다.

**[나의 경험]**

팀원이 한 컬럼안에 리스트화 된 값을 저장하자고 제시하였고, 당시 RDB인 MySQL을 사용 중에 있어
제 1정규형에 위배되어 정규화를 설명 후 데이터 구조 설계를 맡은 경험이 있었습니다.

# 6. ACID가 뭔가요?

### [답변]

트랜잭션의 성질로 원자성, 일관성, 독립성, 영속성을 뜻합니다.

**Atomicity(원자성) All or Nothing**

- 데이터 베이스의 상태가 일관적일 수 있도록 유지
- 트랜잭션의 연산은 데이터베이스에 모두 반영되든지 아니면 전혀 반영되지 않아야 한다.
- 트랜잭션 내의 모든 명령은 반드시 완벽히 수행되어야 하며, 모두가 완벽히 수행되지 않고 어느하나라도 오류가 발생하면 트랜잭션 전부가 취소되어야 한다.

**Consistency(일관성) Consistent**

consistent 상태에서 consistent 상태로 변경되게끔

- 트랜잭션이 그 실행을 성공적으로 완료하면 언제나 일관성 있는 데이터베이스 상태로 변환한다.
- 시스템이 가지고 있는 고정요소는 트랜잭션 수행 전과 트랜잭션 수행 완료 후의 상태가 같아야 한다.

**Isolation(독립성,격리성)**

- 둘 이상의 트랜잭션이 동시에 병행 실행되는 경우 어느 하나의 트랜잭션 실행중에 다른 트랜잭션의 연산이 끼어들 수 없다.
- 수행중인 트랜잭션은 완전히 완료될 때까지 다른 트랜잭션에서 수행 결과를 참조할 수 없다.

**Durablility(영속성,지속성)**

- 성공적으로 완료된 트랜잭션의 결과는 시스템이 고장나더라도 영구적으로 반영되어야 한다.

# 7. RDBMS vs NOSQL에 대해서 설명해주세요.

### [답변]

RDBMS는 정해진 스키마가 존재하고, NoSQL는 정해진 스키마가 없다는 것이 가장 큰 차이입니다. NoSQL은 정해진 스키마가 없을 때 데이터 구조 변화가 자유롭고 데이터 분산이 용이하다는 장점이 있지만, 데이터 중복이 발생하거나 데이터 변경 시에 연산이 오래 걸린다는 단점이 있습니다.

**RDBMS(DataBase Management System)**

- 장점
    - ACID를 지키며 테이블간의 관계가 맺어져있다.
- 단점
    - 유연한 확장성 부족: 새로운 컬럼을 추가한다면 스키마 변경을 해야됨(데이터가 대량이라면 부담)
    - join을 많이 하면 cpu사용도 많이 하고 응답 시간이 길어짐, scale-out에 유연한 db는 아님

**NoSQL 특징**

- flexible schema → application레벨에서 스키마 관리 필요
    - mongo db → json형식으로 데이터를 넣어줌
- 중복 허용(join 회피)
- scale-out 최적화 → 서버 여러 대로 하나의 클러스터를 구성
- acid일부 포기, high-throughput & low-latency 추구

**NoSQL(Not Only SQL)유형**

**Document Database**

- JSON, BSON, XML 같은 문서에 데이터 저장
- 필드와 값의 쌍으로 표현
- 대량의 데이터를 수용하도록 수평 스케일아웃 가능
- MongoDB

**Key-Value Database**

- 각 항목에 키와 값이 포함되어 있음
- 대량의 데이터를 저장해야 하지만 검색을 위해 복잡한 쿼리를 수행할 필요가 없을 때 적합 ex) 사용자 선호도 저장, 캐싱
- Redis, DynanoDB

**Wide-Column Databse**

- 테이블, 행, 동적 열에 데이터 저장
- 각 행이 동일한 열을 가질 필요가 없다 → 관계형보다 뛰어난 유연성 제공
- 대량의 데이터 저장에 적합 ex) 사물인터넷 데이터, 사용자 프로필 데이터
- Cassandra, HBase

**Graph Database**

- 노드와 엣지로 데이터 저장
- 노드: 일반적으로 사람, 장소 및 사물에 대한 정보
- 엣지: 노드 간의 관계에 대한 정보
- Neo4j, JanusGraph

**시대 흐름(NoSQL 등장 요인)**

인터넷 보급이 잘되면서 sns 활성화

high-throughput & low-latency 요구, 비정형 데이터의 증가

# 8. Elastic Search에 대해서 간단히 설명해주세요.

### [답변]

Elastic Search는 텍스트, 숫자, 위치 기반 정보, 정형 및 비정형 데이터 등 모든 유형의 데이터를 위한 무료 검색 및 분석 엔진입니다.

ELK Stack을 직접 관여한건 아니지만 키바나에서 로그를 확인하며 사용하였습니다.

**ELK( Elasticsearch / Logstatsh / Kibana ) Stack**

- **Logstash**
    - 다양한 소스( DB, csv파일 등 )의 로그 또는 트랜잭션 데이터를 수집, 집계, 파싱하여 Elasticsearch로 전달
- **Elasticsearch**
    - Logstash로부터 받은 데이터를 검색 및 집계를 하여 필요한 관심 있는 정보를 획득
- **Kibana**
    - Elasticsearch의 빠른 검색을 통해 데이터를 시각화 및 모니터링

**Elasticsearch 특징**

- **Scale out**
    - 샤드를 통해 규모가 수평적으로 늘어날 수 있음
- **고가용성**
    - Replica를 통해 데이터의 안정성을 보장
- **Schema Free**
    - Json 문서를 통해 데이터 검색을 수행하므로 스키마 개념이 없음
- **Restful**
    - 데이터 CURD 작업은 HTTP Restful API를 통해 수행하며, 각각 다음과 같이 대응합니다.
        
        
        | Data CRUD | Elasticsearch Restful |
        | --- | --- |
        | SELECT | GET |
        | INSERT | PUT |
        | UPDATE | POST |
        | DELETE | DELETE |
        | HEAD(인덱스 정보 확인) |  |

**신속한 가치 실현**

Elasticsearch는 간단한 REST 기반 API, 간단한 HTTP 인터페이스를 제공하고 스키마 없는 JSON 문서를 사용해 다양한 사용 사례에서 쉽게 시작하고 빠르게 애플리케이션을 구축할 수 있습니다.

**고성능**

Elasticsearch의 분산 성질로 인해 대량 볼륨의 데이터를 병렬로 처리할 수 있어 쿼리에 최고의 일치 항목을 빠르게 찾을 수 있습니다.

**무료 도구 및 플러그인**

Elasticsearch는 유명 시각화 및 보고서 도구인 Kibana가 통합되어 제공됩니다. Beats 및 Logstash와의 통합도 제공하여 소스 데이터를 쉽게 전환하고 Elasticsearch 클러스터에 로드할 수 있습니다. 언어 분석기 및 제안자 등 다수의 오픈 소스 Elasticsearch 플러그인을 사용하여 애플리케이션에 풍부한 기능을 추가할 수도 있습니다.

**실시간에 가까운 운영**

데이터 읽기 및 쓰기와 같은 Elasticsearch 운영은 보통 1초도 안 걸려서 완료됩니다. 덕분에 애플리케이션 모니터링 및 이상 탐지와 같은 실시간에 가까운 사용 사례에 Elasticsearch를 사용할 수 잇습니다.

**쉬운 애플리케이션 개발**

Elasticsearch는 Java, Python, PHP, JavaScript, Node.js, Ruby 및 기타 여러 다양한 언어에 대한 지원을 제공합니다.

**사용 사례**

- 애플리케이션 검색
- 웹사이트 검색
- 엔터프라이즈 검색
- 로깅과 로그 분석
- 인프라 메트릭과 컨테이너 모니터링
- 애플리케이션 성능 모니터링
- 위치 기반 정보 데이터 분석 및 시각화
- 보안 분석
- 비즈니스 분석