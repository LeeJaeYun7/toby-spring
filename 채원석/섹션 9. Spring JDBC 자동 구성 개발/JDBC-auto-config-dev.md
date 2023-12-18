# 자동 구성 클래스와 빈 설계
- simpleDriverDataSource가 기본적으로 있지만 실무에서는 거의 안쓰고 써서도 안됨
- HikariDataSource와 @ConditionalOnSingleCandidate
- JDBC template와 JdbcTransactionManager
- in-memory database인 H2

# DataSource 자동 구성 클래스
- forname() 메소드
- SQLexception
- @TestPropertySource
- @ConditionalOnMissingBean

# JdbcTemplate와 트랜잭션 매니저 구성
- JdbcTemplate 클래스
- JdbcTransactionManager() 메소드
- TransactionManagementConfigurationSelector 클래스
- @autoWited과 @BeforeEach
- @Rollback

# Hello 리포지토리
- 
-
-

# 리포지토리를 사용하는 HelloService
-
-
-
