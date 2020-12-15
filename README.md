# jquery_03_20201215
JQuery의 addClass( ~ ), removeClass( ~ ), hover( ~ ) 메소드, 특정 행을 보이거나 사라지게 한다.


      <!-- 
      ~~~~~~~~~~~~~~~~~~~~~~~
      jquery_03.html
      ~~~~~~~~~~~~~~~~~~~~~~~
          => <table> 태그로 표현 되는 행의 배경 색상을 jQuery를 사용하여 지배한다.
          => JQuery의 addClass(~), removeClass(~), hover(~) 메소드 사용법을 숙지한다.     
       -->

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

      <!DOCTYPE html>
      <html>
          <style>
              /*------------------------------------------------------*/
              /* class="style1"이 삽입된 태그에 배경색과 글자색상을 지정 fce5ed*/
              /*------------------------------------------------------*/
              .style1{ background-color : #d5edf7; color: #000000; }
              .style2{ background-color : #fce5ed; color: #000000; }

          </style>


      <!----------------------------------------------------------------->
      <head>
          <meta charset='utf-8'>
          <!-- Jquery 라이브러리 수입. -->
          <script src="jquery-1.11.0.min.js"></script>
          <script>

              //mmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm
              // body 태그 안의 요소를 읽어들인 후 익명함수 내부의 자스코딩을 실행
              //mmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm
              $(document).ready(function(){
                  //--------------------------------------------
                  // id="staff"가 있는 태그의 후손 중, thread 태그 안의 후손 중
                  // 배경색을 gray 색상으로 설정하기
                  //--------------------------------------------
                  // $('#staff thead tr').css({'background':'hotpink','color':'black'});√
                  // $('#staff thead tr').css('background','pink');

                  $('#staff tr:eq(0)').css({'background':'#ED408B','color':'white'});
                      //--------------------------------
                      // 위 코딩은 아래 코딩으로 대체가 가능하다.
                      //--------------------------------
                      // $('tr:eq(0)').css({'background':'black','color':'white'}); //안좋은방법 table 태그 여러개있다면?
                      // $('#staff tr').eq(0).css({'background':'black','color':'white'});
                      // $('table tr').eq(0).css({'background':'black','color':'white'});//안좋은 방법 table 태그 여러개있다면..(역이용한다면 여러테이블똑같이 다 주고싶다면 좋다.)


                  //--------------------------------
                  // id="staff" 가 있는 태그 후손의 <tbody> 후손의 tr 중
                  // 인덱스 번호가 홀수(=사람 입장에선 짝수)인 놈의 배경을 white로 바꿈
                  //--------------------------------
                  $('#staff tbody tr:odd').css('background','white');
                  //--------------------------------
                  // id="staff" 가 있는 태그 후손의 <tbody> 후손의 tr 중
                  // 인덱스 번호가 짝수(=사람 입장에선 홀수)인 놈의 배경을 #EEEEEE 바꿈
                  //--------------------------------
                  $('#staff tbody tr:even').css('background','#EEEEEE');


                  //--------------------------------
                  // id="staff" 가 있는 태그 후손의 <tbody>태그 후손의 각 tr에 마우스를 대면 
                  // 설정한 배경색으로 바꾸고 떼면 원래로 돌아가도록 설정하기
                  //--------------------------------
                      // $('선택자').hover( function(){실행구문1}, function(){실행구문2} );
                      //--------------------------------
                      // 선택자가 가르키는 태그에 마우스 다면 실행구문1 실행, 마우스 빼면 실행구문2 실행하기
                  $("#staff tbody tr").hover(
                      function(){
                          // 마우스를 갖다댄 tr 태그 후손의 td 태그에 class="style1" 삽입함.
                          // class="style1" 삽입함으로써 <style> 태그에 설정한 CSS가 적용됨.
                          // this 는 마우스를 갖다댄 tr 태그를 가리키는 선택자이다.
                          $(this).find("td").addClass("style1");
                      },
                      function(){
                          // 마우스를 갖다댄 tr 태그 후손의 td 태그에 class="style1" 제거.
                          // this 는 마우스를 뺀 tr 태그를 가리키는 선택자이다.
                          $(this).find("td").removeClass("style1");
                      }
                  );


                  //--------------------------------
                  // id="staff" 가 있는 태그 후손의 thead태그 후손의 각 th에 마우스 대면
                  // 그 밑의 tbody 태그 후손의 tr 태그 후손 td의 배경색을 바꾸기
                  // 즉 마우스를 댄 th태그의 밑 즉 세로 방향의 td의 배경색을 바꾸기
                  //--------------------------------
                  $("#staff thead tr th").hover(
                      function(){
                          // 마우스가 올라간 th 태그의 형제 순서번호 구하기
                          //마우스를 갖다댄 태그가 형제중에 몇번째인지 구하는 메소드 index()
                          // 거기에 +1을 해줘야 내가 몇번째인지 알 수 있다.0번째면 +1 => 1번째
                          var no = $(this).index()+1;

                          // tbody 내부의 td 중에 각 td가 속한 부모태그의 
                          // no번째 자식td 태그를 골라 class=style2 를 삽입하기
                          // 즉, 각 tr 안에서 no 번째 td 태그에 class=style2 를 삽입하기
                          $('#staff tbody td:nth-child('+no+')').addClass("style2");
                      },
                      function(){
                          // 뺄땐 그냥 td 안에 있는 css의 style2 놈 다 빼.
                          // 마우스를 때면 class="style2" 속성 제거
                          $('#staff tbody td').removeClass("style2");
                      }
                  );



              });
              //mmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm

          </script>
      </head>

      <!----------------------------------------------------------------->
      <body><center>
          <table id="staff" border="1" cellpadding="5" cellspacing="0" style="border-collapse: collapse;">
              <thead>
                  <tr><th>이름<th>혈액형<th>지역
              </thead>
              <tbody>
                  <tr><td>강민수<td>AB형<td>서울특별시 송파구
                  <tr><td>구지연<td>B형<td>미국 캘리포니아
                  <tr><td>김미화<td>AB형<td>미국 메사추세츠
                  <tr><td>김선화<td>O형<td>서울특별시 강서구
                  <tr><td>남기주<td>A형<td>서울특별시 노량진구
                  <tr><td>윤하린<td>B형<td>서울특별시 용산구
              </tbody>
          </table>

      </body>
      </html>



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ


      <!-- 
      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
      jquery_04.html
      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
          => 특정 행을 보이거나 사라지게 한다.
       -->
      <!DOCTYPE html>
      <html>
      <head>
          <meta charset='utf-8'>
          <script src="jquery-1.11.0.min.js"></script>
          <script>
              //----------------------------------
              // $(document).ready( function(){ 자스코딩 });
              // $.ready( function(){ 자스코딩 });
              // $(function(){ 자스코딩 });
              //----------------------------------
              $(document).ready( function(){ 

                  //----------------------------------
                  // id=movieList 를 가진 태그를 관리하는 JQuery 객체의 메위주를 변수 obj에 저장
                  //----------------------------------
                  var obj = $("#movieList");

                  //----------------------------------
                  // JQuery 객체를 관리하는 태그의 후손 태그 중 짝수 tr 을 관리하는 JQuery 객체 생성하고
                  // hide 메소드 호출하여 짝수행 감추기
                  //----------------------------------
                  obj.find("tr:odd").hide();

                  //----------------------------------
                  // JQuery 객체를 관리하는 태그의 후손 태그 중 짝수 tr 을 관리하는 JQuery 객체 생성하고
                  // hover 메소드 호출하여 마우스 댔을 때 홀수 tr 보이게 하고
                  //                   마우스 빼면 홀수 tr 감추기
                  //---------------------------------- 
                  obj.find("tr:even").hover(
                      function(){

                          // 홀수 tr에 마우스 대면 마우스 댄 tr의 다음 tr만 보이기
                          $(this).next().show()

                      }
                      ,function(){

                          // 홀수 tr에 마우스 빼면 마우스 댄 tr의 다음 tr만 숨기기
                          $(this).next().hide();//시각적으로만 감춤(=hide) 존재함.

                      });
              });




          </script>
      </head>
      <body>
          <table id="movieList" class="movie" border="0" cellpadding="5" width="200" cellspacing="0">
              <tr bgcolor=#da1358>
                  <td><b>로맨틱코미디</b></td>
              </tr>

              <tr bgcolor=#EEEEEE>
                  <td>&nbsp;&nbsp;&nbsp;건축학개론<br>
                      &nbsp;&nbsp;&nbsp;애인있어요<br>
                      &nbsp;&nbsp;&nbsp;500일의썸머
                  </td>
              </tr>
              <tr bgcolor=#f2b008>
                  <td><b>전쟁</b></td>
              </tr>

              <tr bgcolor=#EEEEEE>
                  <td>&nbsp;&nbsp;&nbsp;태극기휘날리며<br>
                      &nbsp;&nbsp;&nbsp;포화속으로<br>
                      &nbsp;&nbsp;&nbsp;공동경비구역JSA
                  </td>
              </tr>

              <tr bgcolor=#5131f4>
                  <td><b>드라마</b></td>
              </tr>

              <tr bgcolor=#EEEEEE>
                  <td>&nbsp;&nbsp;&nbsp;달의연인<br>
                      &nbsp;&nbsp;&nbsp;미스터션샤인<br>
                      &nbsp;&nbsp;&nbsp;뷰티풀마인드
                  </td>
              </tr>

          </table>

      </body>
      </html>

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

      <!-- 
      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
      jquery_04_01.html
      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
          => 특정 행을 보이거나 사라지게 한다.
       -->
       <!DOCTYPE html>
       <html>
       <head>
           <meta charset='utf-8'>
           <script src="jquery-1.11.0.min.js"></script>
           <script>
               //----------------------------------
               // $(document).ready( function(){ 자스코딩 });
               // $.ready( function(){ 자스코딩 });
               // $(function(){ 자스코딩 });
               //----------------------------------
               $(document).ready( function(){ 

                   //----------------------------------
                   // id=movieList 를 가진 태그를 관리하는 JQuery 객체의 메위주를 변수 obj에 저장
                   //----------------------------------
                   var obj = $("#movieList");

                   //----------------------------------
                   // JQuery 객체를 관리하는 태그의 후손 태그 중 짝수 tr 을 관리하는 JQuery 객체 생성하고
                   // hide 메소드 호출하여 짝수행 감추기
                   //----------------------------------
                   obj.find("tr:odd").hide();

                   //----------------------------------
                   // JQuery 객체를 관리하는 태그의 후손 태그 중 짝수 tr 을 관리하는 JQuery 객체 생성하고
                   // hover 메소드 호출하여 마우스 댔을 때 홀수 tr 보이게 하고
                   //                   마우스 빼면 홀수 tr 감추기
                   //---------------------------------- 
                   obj.find("tr:even").hover(
                       function(){

                          obj.find("tr:odd").hide();
                           // 홀수 tr에 마우스 대면 마우스 댄 tr의 다음 tr만 보이기
                           $(this).next().show()


                       }
                       ,function(){

                          // 홀수 tr에 마우스 빼면 마우스 댄 tr의 다음 tr만 숨기기
                          // $(this).next().hide();//시각적으로만 감춤(=hide) 존재함.

                       });
               });




           </script>
       </head>
       <body>
           <table id="movieList" class="movie" border="0" cellpadding="5" width="200" cellspacing="0">
               <tr bgcolor=#da1358>
                   <td><b>로맨틱코미디</b></td>
               </tr>

               <tr bgcolor=#EEEEEE>
                   <td>&nbsp;&nbsp;&nbsp;건축학개론<br>
                       &nbsp;&nbsp;&nbsp;애인있어요<br>
                       &nbsp;&nbsp;&nbsp;500일의썸머
                   </td>
               </tr>
               <tr bgcolor=#f2b008>
                   <td><b>전쟁</b></td>
               </tr>

               <tr bgcolor=#EEEEEE>
                   <td>&nbsp;&nbsp;&nbsp;태극기휘날리며<br>
                       &nbsp;&nbsp;&nbsp;포화속으로<br>
                       &nbsp;&nbsp;&nbsp;공동경비구역JSA
                   </td>
               </tr>

               <tr bgcolor=#5131f4>
                   <td><b>드라마</b></td>
               </tr>

               <tr bgcolor=#EEEEEE>
                   <td>&nbsp;&nbsp;&nbsp;달의연인<br>
                       &nbsp;&nbsp;&nbsp;미스터션샤인<br>
                       &nbsp;&nbsp;&nbsp;뷰티풀마인드
                   </td>
               </tr>

           </table>

       </body>
       </html>


ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ
ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

       <!-- 
      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
      jquery_05.html
      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
          => 라디오 버튼 같은 checkbox 를 만들어보자
          => checkbox 모양이지만 단일 선택만 가능하고 단일 선택된 checkbox는 체크가 풀린다.
       -->
      <!DOCTYPE html>
      <html>
      <head>
          <meta charset='utf-8'>
          <script src="jquery-1.11.0.min.js"></script>
          <script>

              //$(document).ready(function(){자스코딩});
              $(document).ready(function(){

                  // name="hobby" 를 가진 태그에 change 이벤트가 발생하면 실행할 자스코드 설정하기
                  $("[name=hobby]").change(function(){

                      // 제이쿼리 메소드 중 형제를 고르는 메소드가 있다.
                      alert("선택했냐");
                  });

              });

          </script>
      </head>
      <body><center>
          <input type="checkbox" name="hobby" value="독서">독서<br>
          <input type="checkbox" name="hobby" value="운동">운동<br>
          <input type="checkbox" name="hobby" value="여행">여행<br>
          <input type="checkbox" name="hobby" value="수집">수집

      </body>
      </html>
