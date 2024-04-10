# mysql-replication
- mysql replication 테스트
- master db는 writable db로, slave db는 read_only로 설정하여 DB 이중화 설정
- DB의 트랜잭션을 read_only로 설정하면 성능 상승의 이점을 누릴 수 있음
## SLAVE 설정
- ```SQL
  CHANGE MASTER TO MASTER_HOST="{master host}",
  MASTER_USER="root",
  MASTER_PASSWORD="root",
  MASTER_LOG_FILE="{master bin filename}"
  MASTER_LOG_POS={master bin position};  

  START slave;
  ```
    - master host 정보는 docker inspect {network name} 통해서 확인
    - MASTER_LOG_FILE, MASTER_LOG_POS는 master db에서 `SHOW master STATUS;` 로 확인
    - slave db에서 `SHOW slave STATUS\G;` 입력하여 slave 연결 상태 확인
        - ```
          Slave_IO_State: Waiting for source to send event
          Slave_IO_Running: Yes
          Slave_SQL_Running: Yes
          ```
        - 위처럼 나온다면 연결 성공