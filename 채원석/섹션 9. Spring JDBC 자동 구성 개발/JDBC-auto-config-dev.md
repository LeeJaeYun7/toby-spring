# 자동 구성 클래스와 빈 설계
- simpleDriverDataSource
  - 기본적으로 있지만 실무에서는 거의 안쓰고 써서도 안됨 
- HikariDataSource와 @ConditionalOnSingleCandidate
- JDBC template와 JdbcTransactionManager
- in-memory database인 H2

# DataSource 자동 구성 클래스
- forname() 메소드
- SQLexception
  - 대부분 일반적인 throw로는 잡기 어려운 예외이며 런타임/언체크 예외로 전환이 필요
  - 원인들이 여러 개가 있어도 애매하게 알려주는 예외이다.
- @TestPropertySource
- @ConditionalOnMissingBean

# JdbcTemplate와 트랜잭션 매니저 구성
- JdbcTemplate 클래스
- JdbcTransactionManager() 메소드
- TransactionManagementConfigurationSelector 클래스
- @autoWired과 @BeforeEach
  - @AutoWired는 스프링의 컨텍스트 빈 중에서 인스턴스 변수에 주입 가능한 타입의 빈을 찾아준다.
  -  
- @Rollback
  - 테스트 후 트랜잭션이 자동 롤백 되는 것을 방지
  - 롤백의 이유는 원자성이 보존되어야 하는 트랜잭션에서 일부만 상태가 바뀌는 것을 방지함
  - 기본값은 true로 되어있다. 
