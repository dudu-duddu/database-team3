-- 외래 키 검사를 비활성화
SET FOREIGN_KEY_CHECKS = 0;

-- 모든 테이블 삭제
DROP TABLE IF EXISTS 알림;
DROP TABLE IF EXISTS 결제;
DROP TABLE IF EXISTS 객실_숙소정보;
DROP TABLE IF EXISTS 예약;
DROP TABLE IF EXISTS 사업장;
DROP TABLE IF EXISTS 업주;
DROP TABLE IF EXISTS 고객;
DROP TABLE IF EXISTS 회사_고객;
DROP TABLE IF EXISTS 회사;

-- 외래 키 검사를 다시 활성화
SET FOREIGN_KEY_CHECKS = 1;

-- 회사 테이블 생성
CREATE TABLE 회사 (
    회사ID INT AUTO_INCREMENT PRIMARY KEY,
    회사이름 VARCHAR(100) NOT NULL,
    전화번호 VARCHAR(20),
    회사이메일 VARCHAR(100),
    회사대표 VARCHAR(50),
    본사위치 VARCHAR(200)
);

-- 고객 테이블 생성
CREATE TABLE 고객 (
    고객번호 INT AUTO_INCREMENT PRIMARY KEY,
    고객이름 VARCHAR(50) NOT NULL,
    주민등록번호 VARCHAR(20),
    핸드폰번호 VARCHAR(20),
    주소 VARCHAR(200),
    이메일 VARCHAR(100),
    비밀번호 VARCHAR(50),
    회사ID INT,
    FOREIGN KEY (회사ID) REFERENCES 회사(회사ID)
);

-- 업주 테이블 생성
CREATE TABLE 업주 (
    업주번호 INT AUTO_INCREMENT PRIMARY KEY,
    회사이름 VARCHAR(100) NOT NULL,
    업주이름 VARCHAR(50) NOT NULL,
    사업자번호 VARCHAR(50),
    주민등록번호 VARCHAR(20),
    핸드폰번호 VARCHAR(20),
    이메일 VARCHAR(100),
    비밀번호 VARCHAR(50)
);

-- 회사-고객 관계 테이블 생성
CREATE TABLE 회사_고객 (
    회사ID INT,
    고객번호 INT,
    PRIMARY KEY (회사ID, 고객번호),
    FOREIGN KEY (회사ID) REFERENCES 회사(회사ID),
    FOREIGN KEY (고객번호) REFERENCES 고객(고객번호)
);

-- 사업장 테이블 생성
CREATE TABLE 사업장 (
    사업장ID INT AUTO_INCREMENT PRIMARY KEY,
    사업장종류 VARCHAR(50),
    사업장명 VARCHAR(100) NOT NULL,
    업주번호 INT,
    사업장주소 VARCHAR(200),
    방타입 VARCHAR(50),
    FOREIGN KEY (업주번호) REFERENCES 업주(업주번호)
);

-- 예약 테이블 생성
CREATE TABLE 예약 (
    예약번호 INT AUTO_INCREMENT PRIMARY KEY,
    결제방식 VARCHAR(50),
    인원수 INT,
    예약시작일 DATE,
    일렬번호 INT,
    고객번호 INT,
    FOREIGN KEY (고객번호) REFERENCES 고객(고객번호)
);

-- 객실/숙소 정보관리 테이블 생성
CREATE TABLE 객실_숙소정보 (
    숙소ID INT AUTO_INCREMENT PRIMARY KEY,
    객실ID INT,
    숙소명 VARCHAR(100),
    숙소유형 VARCHAR(50),
    위치 VARCHAR(100),
    객실유형 VARCHAR(50),
    최대수용인원 INT,
    가격 DECIMAL(10, 2),
    예약가능여부 BOOLEAN,
    부가시설 VARCHAR(200)
);

-- 결제 시스템 테이블 생성
CREATE TABLE 결제 (
    결제ID INT AUTO_INCREMENT PRIMARY KEY,
    예약ID INT,
    금액 DECIMAL(10, 2),
    결제방법ID INT,
    날짜 DATE,
    FOREIGN KEY (예약ID) REFERENCES 예약(예약번호)
);

-- 알림 시스템 테이블 생성
CREATE TABLE 알림 (
    알림ID INT AUTO_INCREMENT PRIMARY KEY,
    고객ID INT,
    업주ID INT,
    알림유형ID INT,
    메시지 VARCHAR(255),
    날짜 DATE,
    FOREIGN KEY (고객ID) REFERENCES 고객(고객번호),
    FOREIGN KEY (업주ID) REFERENCES 업주(업주번호)
);

-- 이벤트/행사 관리 테이블 생성
CREATE TABLE 이벤트_행사 (
    이벤트ID INT AUTO_INCREMENT PRIMARY KEY,
    이벤트이름 VARCHAR(100),
    시작일자및시간 DATETIME,
    종료일자및시간 DATETIME,
    설명 TEXT,
    장소ID INT
);

-- 예시 데이터 삽입

-- 회사 데이터 삽입
INSERT INTO 회사 (회사이름, 전화번호, 회사이메일, 회사대표, 본사위치)
VALUES 
    ('ABC 숙박', '02-1234-5678', 'abc@example.com', '홍길동', '서울 강남구'),
    ('XYZ 호텔', '02-9876-5432', 'xyz@example.com', '이순신', '서울 중구');

-- 고객 데이터 삽입
INSERT INTO 고객 (고객이름, 주민등록번호, 핸드폰번호, 주소, 이메일, 비밀번호, 회사ID)
VALUES 
    ('김철수', '950101-1234567', '010-1111-2222', '서울 강서구', 'kim@example.com', 'password123', 1),
    ('이영희', '960202-2345678', '010-3333-4444', '경기 성남시', 'lee@example.com', 'pass456', 2);

-- 업주 데이터 삽입
INSERT INTO 업주 (회사이름, 업주이름, 사업자번호, 주민등록번호, 핸드폰번호, 이메일, 비밀번호)
VALUES 
    ('ABC 숙박', '홍길동', '1234567890', '900101-1234567', '010-1111-2222', 'hong@example.com', 'pass789'),
    ('XYZ 호텔', '이순신', '9876543210', '910202-2345678', '010-3333-4444', 'lee@example.com', 'passabc');

-- 회사-고객 관계 데이터 삽입
INSERT INTO 회사_고객 (회사ID, 고객번호)
VALUES 
    (1, 1),
    (2, 2);

-- 사업장 데이터 삽입
INSERT INTO 사업장 (사업장종류, 사업장명, 업주번호, 사업장주소, 방타입)
VALUES 
    ('호텔', 'ABC 호텔 서울점', 1, '서울 강남구 역삼동', '스위트룸'),
    ('모텔', 'XYZ 모텔 분당점', 2, '경기 성남시 분당구', '프리미엄룸');

-- 예약 데이터 삽입
INSERT INTO 예약 (결제방식, 인원수, 예약시작일, 일렬번호, 고객번호)
VALUES 
    ('카드결제', 2, '2023-07-01', 1, 1),
    ('현금결제', 1, '2023-08-15', 2, 2);

-- 객실/숙소 정보관리 데이터 삽입
INSERT INTO 객실_숙소정보 (객실ID, 숙소명, 숙소유형, 위치, 객실유형, 최대수용인원, 가격, 예약가능여부, 부가시설)
VALUES 
    (1, 'ABC 호텔 서울점', '호텔', '서울 강남구 역삼동', '스위트룸', 4, 300000, TRUE, 'WiFi, TV, 에어컨'),
    (2, 'XYZ 모텔 분당점', '모텔', '경기 성남시 분당구', '프리미엄룸', 2, 150000, TRUE, 'WiFi, TV');

-- 결제 데이터 삽입
INSERT INTO 결제 (예약ID, 금액, 결제방법ID, 날짜)
VALUES 
    (1, 300000, 1, '2023-07-01'),
    (2, 150000, 2, '2023-08-15');

-- 알림 시스템 데이터 삽입
INSERT INTO 알림 (고객ID, 업주ID, 알림유형ID, 메시지, 날짜)
VALUES 
    (1, 1, 1, '예약이 완료되었습니다.', '2023-07-01'),
    (2, 2, 2, '결제가 완료되었습니다.', '2023-08-15');

-- 이벤트/행사 관리 데이터 삽입
INSERT INTO 이벤트_행사 (이벤트이름, 시작일자및시간, 종료일자및시간, 설명, 장소ID)
VALUES 
    ('여름 할인 이벤트', '2023-07-01 10:00:00', '2023-07-31 23:59:59', '여름 시즌 할인 이벤트입니다.', 1),
    ('가을 축제', '2023-09-01 10:00:00', '2023-09-10 23:59:59', '가을 맞이 축제 행사입니다.', 2);
    
-- 회사 테이블 데이터 조회
SELECT * FROM 회사;

-- 고객 테이블 데이터 조회
SELECT * FROM 고객;

-- 업주 테이블 데이터 조회
SELECT * FROM 업주;

-- 회사_고객 테이블 데이터 조회
SELECT * FROM 회사_고객;

-- 사업장 테이블 데이터 조회
SELECT * FROM 사업장;

-- 예약 테이블 데이터 조회
SELECT * FROM 예약;

-- 객실_숙소정보 테이블 데이터 조회
SELECT * FROM 객실_숙소정보;

-- 결제 테이블 데이터 조회
SELECT * FROM 결제;

-- 알림 테이블 데이터 조회
SELECT * FROM 알림;

-- 이벤트_행사 테이블 데이터 조회
SELECT * FROM 이벤트_행사;
