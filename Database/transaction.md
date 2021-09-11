## 트랜잭션이란?

- 트랜잭션(Transaction 이하 트랜잭션)이란, 데이터베이스의 상태를 변화시키기 해서 수행하는 작업의 단위를 뜻한다.

## **트랜잭션의 특징**

---

********트랜잭션의 특징은 크게 4가지로 구분된다.

- 원자성 (Atomicity)
- 일관성 (Consistency)
- 독립성 (Isolation)
- 지속성 (Durability)

첫번째로, 원자성은 트랜잭션이 데이터베이스에 모두 반영되던가, 아니면 전혀 반영되지 않아야 한다는 것이다.  트랜잭션은 사람이 설계한

논리적인 작업 단위로서, 일처리는 작업단위 별로 이루어 져야 사람이 다루는데 무리가 없다.

만약 트랜잭션 단위로 데이터가 처리되지 않는다면, 설계한 사람은 데이터 처리 시스템을 이해하기 힘들 뿐만 아니라, 오작동 했을시 원인을 찾기가 매우 힘들어질것이다.

두번째로, 일관성은 트랜잭션의 작업 처리 결과가 항상 일관성이 있어야 한다는 것이다.

트랜잭션이 진행되는 동안에 데이터베이스가 변경 되더라도 업데이트된 데이터베이스로 트랜잭션이 진행되는것이 아니라,

처음에 트랜잭션을 진행 하기 위해 참조한 데이터베이스로 진행된다. 이렇게 함으로써 각 사용자는 일관성 있는 데이터를 볼 수 있는 것이다.

세번째로, 독립성은 둘 이상의 트랜잭션이 동시에 실행되고 있을 경우 어떤 하나의 트랜잭션이라도, 다른 트랜잭션의 연산에 끼어들 수 없다는 점을 가리킨다.

하나의 특정 트랜잭션이 완료될때까지, 다른 트랜잭션이 특정 트랜잭션의 결과를 참조할 수 없다.

네번째로, 지속성은 트랜잭션이 성공적으로 완료됬을 경우, 결과는 영구적으로 반영되어야 한다는 점이다.

# **트랜잭션 연산 및 상태**

**Commit연산**

**1.** Commit 연산은 한개의 논리적 단위(트랜잭션)에 대한 작업이 성공적으로 끝났고 데이터베이스가 다시 일관된 상태에 있을 때, 이 트랜**2.** 잭션이 행한 갱신 연산이 완료된 것을 트랜잭션 관리자에게 알려주는 연산이다.

**Rollback연산**

**1.** Rollback 연산은 하나의 트랜잭션 처리가 비정상적으로 종료되어 데이터베이스의 일관성을 깨뜨렸을 때, 이 트랜잭션의 일부가 정상적으로 처리되었더라도 트랜잭션의 원자성을 구현하기 위해 이 트랜잭션이 행한 모든 연산을 취소(Undo)하는 연산이다.

**2.** Rollback시에는 해당 트랜잭션을 재시작하거나 폐기한다.

**트랜잭션의 상태**

[https://t1.daumcdn.net/cfile/tistory/999C55345B6D2ED308](https://t1.daumcdn.net/cfile/tistory/999C55345B6D2ED308)

**활동(Active) :** 트랜잭션이 실행중인 상태

**실패(Failed) :** 트랜잭션 실행에 오류가 발생하여 중단된 상태

**철회(Aborted) :** 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태

**부분 완료(Partially Committed) :** 트랜잭션의 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태

**완료(Committed) :** 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태

### 트랜잭션 예제

```sql
BEGIN TRAN -- 트랜잭션 시작

-작업-

ROLLBACK TRAN -- 트랜잭션 이전상태로 ROLL BACK

COMMIT TRAN -- 트랜잭션 완료
```

### **Transaction Isolation Levels**

- 트랜잭션에서 일관성이 없는 테이터를 허용하도록 하는 수준

The degree to which the results of one transaction are visible to other transactions is known as the transaction isolation level. You can set the isolation level on a per-transaction basis. The following four levels are defined in the SQL standard:

SERIALIZABLE

- This is the default specified by the SQL standard. Dirty reads, non-repeatable reads, and phantom reads are not permitted in this isolation level. SERIALIZABLE is the most "strict" of the isolation levels.

REPEATABLE READ (mysql, mariadb, db2)

- Dirty reads and non-repeatable reads are not permitted, but phantom reads are permitted. This isolation level is not supported by Oracle.

> 팬텀리드

READ COMMITTED (Oracle, postgresql, mssql)

- This is the default used by Oracle. Dirty reads are not permitted, but non-repeatable reads and phantom reads are permitted.

> 논 리피터블 리드

READ UNCOMMITTED (mongodb)

- Dirty reads, non-repeatable reads, and phantom reads are permitted. This isolation level is not supported by Oracle.

> 더티리드

### Propagation (전파 속성)

[[Spring] 트랜잭션의 전파 설정별 동작](https://deveric.tistory.com/86)

### 참조

[https://mommoo.tistory.com/62](https://mommoo.tistory.com/62)

[https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation](https://nesoy.github.io/articles/2019-05/Database-Transaction-isolation)

[https://oingdaddy.tistory.com/28](https://oingdaddy.tistory.com/28)

[https://goddaehee.tistory.com/167](https://goddaehee.tistory.com/167)