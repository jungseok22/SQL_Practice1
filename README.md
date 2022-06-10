# SQL_Practice1

sql 6.10 practice 



USE SQLDB; 
select * from usertbl; 
select * from usertbl where name = '김경호'; 
select * from usertbl where birthyear >=1970 and birthyear <=1988 ;

select name as 이름, addr as 주소 from usertbl where height>= 170;

select name, height from usertbl where height >=  All (select height from usertbl where addr = '경남'); 

select name , mDate from usertbl order by mdate desc;  -- 내림차순
select name , mDate from usertbl order by mdate asc;   -- 오름차순

select addr from usertbl; -- 중복많음
select distinct addr from usertbl;  -- 중복없애고 하나씩만 보여주기

select * from buytbl limit 5;  -- 제일 앞 5건만 출력하기
create table buytbl2 (select * from buytbl); -- 테이블 복사하기
select * from buytbl2; 

select userid, amount from buytbl order by userid; -- userid와 amount 뽑아서 정렬하는데 userid 정렬
select userid as '사용자 아이디', sum(amount) as '총 구매 개수'  from buytbl group by userid; -- userid를 그룹별로 묶고 amount를 집계함수 sum을 사용해 한번에 계산

select userid 사용자 , sum(price*amount) 총구매액 from buytbl 
	group by userid
    having sum(price*amount) > 100;   -- where절에서 집계함수를 쓸수 없어서 having으로 대체가능! 단 group by절 다음에 나와야함
    
select * from testtbl3;
create table testtbl3(id int, username char(4), age int); -- 테이블 만들고 설정
insert into testtbl3 values(1, '이정석', 10); -- 테이블에 데이터삽입
insert into testtbl3(username,id) values ('하니',2); -- 삽입순서 혹은 열순서를 다르게 입력 시 테이블 명 뒤에 반드시 추가내용 적기
-- 수정 시 update 테이블명 set 열1=값1,열2=값2...... where 조건;  
-- 삭제 시 delete from 테이블이름 where 조건; 

set @myVar1 = 5; -- 변수의 사용
set @myVar2 = 3;
set @myVar3 = 4.25;
set @myVar4 = '가수 이름==> ';

select @myvar1 ;  -- 변수 값 출력
select @myVar4 , name from usertbl where height > 180;  -- 일반적인 select, from 문과 함꼐 사용가능

-- 데이터 형식 변환함수 cast() , convert() 
select avg(amount) as '평균 구매 개수' from buytbl; 
select cast(avg(amount) as signed integer) '평균 구매 개수' from buytbl; 
select convert(avg(amount) , signed integer) '평균 구매 개수' from buytbl; -- 두가지 다 결과는 같음

-- sql 내장함수!!!
select if(100>200 , '참', '거짓임' );
select ifnull(null, '널이군'), ifnull(100, '널이군'); -- 수식1이 null이 아니면 
