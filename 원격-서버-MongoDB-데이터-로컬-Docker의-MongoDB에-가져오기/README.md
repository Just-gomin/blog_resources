# 💡 원격 서버 mongodb 데이터, 로컬 docker의 mongodb에 가져오기

이 글은 기존 MongoDB의 일부 Collection들에 대해 Field를 변경하는 작업을 진행해보기 위해
원격 서버에 있는 MongoDB의 데이터를, 로컬 환경의 Docker MongoDB Container로
가져와 다뤄보기 위해 진행한 과정을 작성 했습니다.

## 📌 1. 원격 서버의 MongoDB 데이터 Dump 생성하기

원격 서버에  ssh 접속합니다.

MongoDB에 있는 데이터를 가져오기 위해서
원격 서버에 있는 데이터에 대해 Dump를 생성해야 합니다.

### 👉 mongodump 실행

- [mongodump](https://www.mongodb.com/docs/database-tools/mongodump/)

```shell
mongodump --out=[dump가_위치하길_바라는_경로]
```

- dump한 날짜를 명시하기 위해 디렉토리에 명시했습니다.

```text
/home/[USER]/dump
  ㄴ dump_20231229
```

mongodump 시 결과물 경로 외에 다른 옵션을 주지 않았고 그 결과
dump_20231229 디렉토리 하부에 데이터베이스 이름의 디렉토리들이 있고,
그 하부에 json과 bson 파일들이 여럿 생성 됐습니다.

## 📌 2. Dump 파일 로컬 PC로 가져오기

Dump 파일을 가져오기 위해서 [Termius](https://termius.com/)라는 툴을 이용해
원격 서버에 SFTP 연결을 통해 파일을 다운로드 했습니다.

## 📌 3. MongoDB Container 실행

내 PC에서 Docker로 MongoDB 컨테이너를 실행 시켰습니다.

```shell
docker run -d -it -p 27017:27017 --name mongodb mongo
```

컨테이너의 이름은 `mongodb`로 지정했습니다.

## 📌 4. MongoDB Container에 Dump 파일 복사하기

mongodb 컨테이너의 `/home` 경로에 dump_20231229를 복사해줍니다.

```shell
docker cp dump_20231229 mongodb:/home
```

## 📌 5. MongoDB Container에 접근해 Restore 진행하기

mongodb 컨테이너의 bash로 접근합니다.

```shell
docker exec -it mongodb bash
```

### 👉 mongorestore 실행

`mongorestore`를 통해 dump 해온 데이터를 MongoDB로 넣어줍니다.

- [mongorestore](https://www.mongodb.com/docs/database-tools/mongorestore/)

```shell
mongorestore /home/dump_20231229
```
