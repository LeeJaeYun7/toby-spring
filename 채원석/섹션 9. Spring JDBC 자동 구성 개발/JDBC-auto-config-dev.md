# 자동 구성 클래스와 빈 설계
- simpleDriverDataSource
  - 기본적으로 있지만 실무에서는 거의 안쓰고 가능한 한 써서도 안됨
- @ConditionalOnSingleCandidate
  - datasource bean이 한개만 있으면 그걸 등록시켜준다.
- JDBC template와 JdbcTransactionManager
  - template은 고정된 작업 흐름을 가진 코드를 재사용하는 의미
  - callback은 그러한 템플릿 안에서 호출되는 걸 목적으로 만든 오브젝트
- in-memory database인 H2
  - 메모리 내부에서 저장소를 만들기에 속도가 빠르다.
  - 내장형과 서버형으로 두 가지로 구성된다.  

# DataSource 자동 구성 클래스
- SQLexception
  - 대부분 일반적인 throw로는 잡기 어려운 예외이며 런타임/언체크 예외로 전환이 필요
  - 원인들이 여러 개가 있어도 애매하게 알려주는 예외이다.
- @TestPropertySource
  - 메타어노테이션으로 부트의 설정을 강제로 바꿔야 할때 필요하다.
  - 가급적 쓸 일은 거의 없는 것이 좋다. 
- @ConditionalOnMissingBean
  - 이미 등록된 같은 타입의 빈이 있으면 넘어가도록 한다. 

# JdbcTemplate와 트랜잭션 매니저 구성
- JdbcTemplate 클래스
  - Jdbc 기능의 템플릿 역할을 하는 클래스
- JdbcTransactionManager() 메소드
  - 예외로는 DataAccessException을 내보낸다. 
- TransactionManagementConfigurationSelector 클래스
  - @transaction 3가지를 구분해서 선택하는 역할을 한다.
  - 주로 @import({TransactionManagementException.class})과 같은 표현으로 사용된다.
- @autoWired과 @BeforeEach
  - @AutoWired는 스프링의 컨텍스트 빈 중에서 인스턴스 변수에 주입 가능한 타입의 빈을 찾아준다.
  ```
  @Autowired
  SimpleDriverDataSource dataSource;
  ```
  - @BeforeEach는 주로 테스트에서 자동으로 메소드를 실행하게 해주는 역할을 한다. 
- @Rollback
  - 테스트 후 트랜잭션이 자동 롤백 되는 것을 방지
  - 롤백의 이유는 원자성이 보존되어야 하는 트랜잭션에서 일부만 상태가 바뀌는 것을 방지함
  - 기본값은 true로 되어있다. 
