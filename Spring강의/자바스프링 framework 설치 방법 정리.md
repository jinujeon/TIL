자바/스프링 framework 설치 방법 정리

1. jdk파일 설치하기 (jdk버전 = jre1.8.0_251)
2. 이클립스 설치 jee-2020-06 (Eclipse IDE for Enterprise Java Developers )
	
	- (https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2020-06/R/eclipse-jee-2020-06-R-win32-x86_64.zip)
3. 오라클 다운 후 알집풀고 setup파일 실행(이클립스와 연동하는 oracle6_g.jar파일(예비용) 이클립스에 넣기)
	
	- (https://www.oracle.com/database/technologies/xe-prior-releases.html)
4. 오라클 첫 db페이지 만들고 설정하기(setup할 당시 설정했던 비밀번호 111111사용)
	- (http://127.0.0.1:8080/apex/f?p=4950)
	sql문 실행 화면
	- (http://127.0.0.1:8080/apex/f?p=4550:1:3393740386859616::::FSP_AFTER_LOGIN_URL:\f?p=4500|1003|7945541006329060||NO|||\)
5. apache-tomcat 다운 후 압축풀기. 이후 폴더를 c드라이브(아무곳이나 괜찮지만 공통 사용위해)에 옮김
6. 이클립스에서 help들어간 후 Eclipse market들어가서 sts검색 후 Spring Tools 4(4.7.1) , Spring Tools 3 (3.9.13)설치  (안되면 Add-On for Spring까지 설치)
7. 프로젝트 생성

	Spring 프로젝트 생성 방식

	1. Project 생성
	2. maven - pom.xml(모든 library 저장 및 설치)
	3. Spring Nature로 바꾸기
	4. src - myspring.xml 설정
	5. Table 구축
	6. 


	프로젝트 생성방식 복습
	
	1. Dynamic Web Project생성
	2. Maven Project (POM.xml)생성
		- ojdbc.jar 별도로 setting(Web)
	3. Spring nature 설정
	4. Biz, Dao Setting
	
	Spring MVC설정
	5. web.xml 수정
	6. spring.xml 수정(WEB-INF에서 config폴더 설정)








Spring 공부내용

1. Spring IoC(Inversion Of Control) - (DI)
	- XML(역주입을 xml에 기입한다.)
	- Annotation(xml이 아니라 객체에 @로서 기입한다.)
	
	1-1. DI
		- Constructor
		- setter
		- p

2. Spring AOP(Aspect Oriented Program)	//함수 실행할 때 항상 실행하는 로그나 예외처리등을 일괄처리할수있도록 정리해줌
	-XML(복잡 어렵)
	-Annotation(간단 간결 선호도 높다)
	
3. Mybatis - ORM(Object Relation Management)
4. Spring MVC













web client : html5, css3, javascript, jquery, ajax
web server : servlet & jsp, spring	

big data : linux

웹서버 아파치 
웹어플리케이션 서버 톰캣

jsp는 서버사이드에서 클라이언트용 화면을 만드는 역할이 주된 역할이다

jstl:if else if


1. Dynamic Web Project (생성)
2. Lidrary - jdbc, jstl	(WEB-INF폴더 아래 lib에 필요 라이브러리 넣기)
3. web.xml	(경로 설정)
4. DispatcherServlet
5. *.mc(hhh.mc 페이지나 xxx.mc페이지 등 앞에 무슨 문자가 오든 상관없이 한곳으로 보냄)
6. index.html (첫번째 페이지 만들기)
7. *.jsp
8. Servlet

int i = 10;

[{key : value, key2 : value2},{},{}];
{"stockdata" : ["버거1", "맥스파이시"],
"asdfaedfae" : [asdifjaosief]
}
{"id" : asdf}'