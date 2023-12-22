# 자동 구성 결과 확인
- ConditionEvaluationReport.class
  - 구성 상태를 기록하는 역할을 하는 클래스
- getConditionAndOutcomesBySource() 
  - .entryset() : map.java에 포함된 메서드, k-v 형식의 맵셋을 리턴
    - .stream() : 연속적인 스트림을 리턴 
- jmx : 스프링 컨테이너 모니터링하는 방법
  - 응용 프로그램 등을 관리/감시 위한 java api
  ![image](https://github.com/1suckk/toby-spring-boot/assets/108579242/820d0ae7-6188-4ef9-be33-d4cd7785bf2f)

# Core 자동 구성 살펴보기
- AopAutoConfiguration.java
  - matchifMissing = true -> 아무 설정이 안되도 실행하는 걸로 체크
  - BeanFactoryPostProcessor -> 클래스 방식의 프록시
- SimpleCacheConfiguration.java
  - @Cacheable 애노테이션을 사용
  - Redis 등 유명한 방법도 소개(스프링 레퍼런스 참조)
- TaskExecutionAutoConfiguration.java
  ```
  @ConditionalOnMissingBean(Executor.class)
	  public ThreadPoolTaskExecutor applicationTaskExecutor(TaskExecutorBuilder builder) {
		  return builder.build();
	  } //ThreadPoolTaskExecutor라는 bean을 return.
  ```
- TaskExecutionProperties.java
  - public int coresize = 8; //한번에 실행이 가능한 코어가 8개까지만 사용 가능
  
# Web 자동 구성 살펴보기
- HttpMessageConvertersAutoConfiguration.java 
  - 메시지 컨버터 : json 파싱, 응답에 body 생성  
- RestTemplateAutoConfiguration.java 
  - RestTemplateBulder bean을 생성
- ServletWebServerFactoryCustomizerAutoConfiguration.java 
  - properties를 주입받은 customizer를 이용해서 factory 형식을 리턴

# Jdbc 자동 구성 살펴보기
- PersistenceExceptionTranslationPostProcessor.java 
  - 예외를 발생하면 추상화해주는 기능을 수행
- DataSourceAutoConfiguration.java 
  - datasource를 만들어주는 기능을 수행
  - hikaridatasource를 연결해주고 없으면 그냥 datasource로 불러오기
- DataSourceTransactionManagerAutoConfiguration.java 
  - 트랜잭션은 원자성이 보장되는 작업
  - 트랜잭션 관리해주는 역랗 수행 (데이터베이스)
- JdbcTemplateAutoConfiguration.java 
  - JdbcTemplate을 만들어주는 자동 구성
- TransactionTemplateConfiguration.java 
  - TransactionTemplate을 설정해서 트랜잭션의 시작과 끝을 제어할 수 있게 해주는 자체적인 bean
