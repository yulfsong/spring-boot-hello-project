# spring boot hello_project
## spring boot MVC게시판 & 로그인 / 카카오 API로그인



목적 : (TMI 주의)
과거에 학원을 다녔을때 요즘은 잘 사용하지 않는 오래된 방식으로 
이클립스 게시판을 만든 적이 있다.
요즘은 학원에서도 스프링부트를 배운다던데,
내가 학원에 다닐때는 못배웠고, 회사로 바로 들어가서 만난 스프링부트는 신세계였다.
하지만 바쁜 일정으로 게시판을 만들일이 없다가
일을 쉬면서 스스로 복기하는 의미해서 스프링부트 버젼으로 게시판을 만들었다.
생각보다 스프링부트 버전으로 만든 게시판이 없어서 초반에 설정때문에 약간 애먹었다.

*요약 : 스스로 복기하는 의미해서 스프링부트 버젼으로 게시판을 만들었다.


***

#### 1. 환경 구성 : 
+ Server OS : Windows 10
+ Spring boot Framework : 2.1.4.RELEASE
+ java version : 1.8
+ build tool : maven 4.0.0
+ Language : JAVA 1.8
+ WEB Server : Apache 
+ WAS Server : Tomcat 7
+ DB : MySQL 5.7.22(navicat)
+ ORM : mybatis 2.1.1

#### 2. 기능 :
+ MVC게시판 CRUD

##### /boardList
/boardList에서는 오로지 페이징처리에만 집중할 수 있도록 하였다.
한번에 10개의 글까지 볼 수 있고, 그 이상이면 넘어가며 
시작번호, 끝번호, 이전, 다음등이 표시된다.
리스트처리는 boardList?stateCode="+stateCode 
이런식으로 무조건 세션에서 가지고온 
멤버상태에 따른 코드를 파라미터로 잡고 화면으로 들어올 수 있게 하였다.

###### /boardWriteForm(get), /boardWrite(post)
/boardWriteForm는 글쓰기폼 뷰를 리턴한다.
현재 session이 일반회원인지, 카카오회원인지에 따라 상태값이 달라지며
제대로 입력하지 않을시 넘어가지 않도록 했고, 
input type을 hidden으로 지정해서 드러내지 않고 stateCode를 보내도록 하였다.

###### /boardRead
글번호인 num을 이용하여 해당 글을 보여주도록 함

###### /boardModifyForm(get), /boardModify(post)
글수정시 카카오유저인지 일반유저인지에 따라 
기본으로 바인딩되는 boardVO의 writer값을 새로 세팅하는 형태로 진행하였다.
우선 session을 통해 해당 일반멤버, 카카오멤버가 있는지를 확인하고
있는 경우 일반멤버, 카카오멤버 둘중 어디라도
글을쓴 아이디와 맞을 경우 수정이 가능하도록 하였다.
일반멤버의 아이디와 카카오멤버의 이메일이 같을 경우는 따로 처리하지 않았다.

###### /boardDelete
글삭제시 현재 접속한 멤버와 글작성자가 맞는지를 판단하고 
맞는 경우만 글을 삭제할 수 있도록 처리하였다.
또한, 편의를 위해 맞을때 ModelAndView를 통해 메시지를 따로 저장하여 
forward로 boardList로 이동한뒤 메시지에 따라 alert를 띄우게 하였다.


