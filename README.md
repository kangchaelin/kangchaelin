![header](https://capsule-render.vercel.app/api?type=waving&color=timeGradient&text=Welcome%20to%20채린's%20GitHub%20🙌&animation=twinkling&fontSize=35&fontAlignY=40&fontAlign=50&height=250)

## 💡 Once I've used
<div style="display:flex; flex-direction:column; align-items:flex-start;">
    <!-- Backend -->
    <p><strong>Backend</strong></p>
    <div>
      <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=Python&logoColor=white">
        <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=Java&logoColor=white"> 
        <img src="https://img.shields.io/badge/Spring-6DB33FF?style=for-the-badge&logo=spring&logoColor=white">
    </div>
      <!-- Frontend -->
    <p><strong>Frontend</strong></p>
    <div>
        <img src="https://img.shields.io/badge/html5-E34F26?style=flat-square&logo=html5&logoColor=white"> 
        <img src="https://img.shields.io/badge/css-1572B6?style=flat-square&logo=css3&logoColor=white"> 
        <img src="https://img.shields.io/badge/javascript-F7DF1E?style=flat-square&logo=javascript&logoColor=black"> 
        <img src="https://img.shields.io/badge/bootstrap-7952B3?style=flat-square&logo=bootstrap&logoColor=white">
        <img src="https://img.shields.io/badge/jQuery-0769AD?style=flat-square&logo=jQuery&logoColor=white">
    </div>
    <!-- Database -->
    <p><strong>Database</strong></p>
    <div>
        <img src="https://img.shields.io/badge/oracle-F80000?style=for-the-badge&logo=oracle&logoColor=white"> 
        <img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white"> 
    </div>
    <!-- Server -->
    <p><strong>Server</strong></p>
    <div>
        <img src="https://img.shields.io/badge/apache tomcat-F8DC75?style=for-the-badge&logo=apachetomcat&logoColor=black">
    </div> 
</div><br>
</div>


## 💡 프로젝트 경험 
### 📌YOU & I
> 클라우드 기반 공통 취미를 공유하는 지역 소모임 관리 플랫폼
- [click me!](https://github.com/2023-SMHRD-IS-CLOUD-1/YOU-I)

</br>

#### 1. 제작 기간 & 참여 인원
- 2023년 11월 22일 ~ 12월 8일
- 팀 프로젝트(5명)

</br>

#### 2. 사용 기술
##### `Back-end`
  - Java

##### `Front-end`
  - HTML
  - JS
  - CSS
    
##### `Data & Server`
  - AWS
  - ORACLE
  - Apache Tomcat

##### `IDE & Etc`
  - GitHub
  - Eclipse
    
</br>

#### 3. 구현 기능
<details><summary><h5>📍 회원 정보 수정</h5></summary>
<div><h6>mypg.html</h6></div>
<div markdown="1">

    // 수정 버튼을 클릭하면 이벤트 발생
    $("#mybtn").on("click", () => {

	var inputValues = [];

 	// input태그(닉네임, 연락처, 활동지역)에 정보를 입력받고, 입력받은 데이터를 inputValues 리스트에 추가
	$(".ip").each(function() {
		var value = $(this).val();
		inputValues.push(value);
	});
 
	var mypCtValues = [];

 	// select태그에 정보를 입력받고, 입력받은 데이터를 mypCtValues 리스트에 추가
	$(".mypCt").each(function() {
		var value = $(this).val();
		mypCtValues.push(value);
	});

	var sendObj = { nick: inputValues[0], phone: inputValues[1], region: inputValues[2], ct1: mypCtValues[0]};
	$.ajax({
		// UpdateMyPage.do페이지에 요청
		url: "UpdateMyPage.do",
  		// UpdateMyPage.do페이지에 데이터 보내기
		data: sendObj,
		dataType: "json",
		success: function() {
		},
		error: function(e) {
		}
		})
	})

</div>

<div><h6>UpdateMyPageService.java</h6></div>
<div markdown="1">
		
		public class UpdateMyPageService implements Command {
		@Override
		public String execute(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
	
			request.setCharacterEncoding("utf-8");
			response.setContentType("text/html;charset=utf-8");
			
			HttpSession session = request.getSession(); 
			String user_id = (String) session.getAttribute("id");
			String nick =request.getParameter("nick");
			String phone =request.getParameter("phone");
			String region =request.getParameter("region");
			String ct1 =request.getParameter("ct1");
	  
			User_DTO u_dt = new User_DTO();
			u_dt.setId(user_id);
			u_dt.setNick(nick);
			u_dt.setPhone(phone);
			u_dt.setRegion(region);
			u_dt.setHobby(ct1);
			
			User_DAO dao = new User_DAO();
			int row = dao.update(u_dt);
			
			if(row > 0 ) {
				return "redirect:/Gomypg.do";
			}
			else {
				return "redirect:/Gomypg.do";
			}
			
		}
	
	   }
    
</div>

<div><h6>User_DAO : update()</h6></div>
<div markdown="1">
	
	public int update(User_DTO dto) {
		SqlSession sqlSession = factory.openSession(true);
		int row = sqlSession.update("update", dto);
		sqlSession.close();
		return row;
	}

</div>

<div><h6>Mapper.xml : id="update"</h6></div>
<div markdown="1">
	
	<update id="update" parameterType="com.YOU_I.model.User_DTO">
		UPDATE tbl_user
		SET
		nick=#{nick}, phone=#{phone}, region=#{region}, hobby=#{hobby}
		WHERE id = #{id}
	</update>

</div>
 </details>

 <details><summary><h5>📍 회원 탈퇴</h5></summary>
<div><h6>mypg.html</h6></div>
<div markdown="1">

    // 탈퇴 버튼을 클릭하면 이벤트 발생
    $("#popupsub").on("click", function() {
    
		var sendObj = { id: $("#userId").val(), pw: $("#userPw").val() };
		$.ajax({

			url: "unregister.do",
			data: sendObj,
			dataType: "json",
			success: function() {

				alert("회원탈퇴에 성공하셨습니다. 이용해주셔서 감사합니다.");
				window.location.href = 	"http://localhost:8081/YOU_I/Gomainpg.do";
			},
			error: function(e) {
				alert("아이디와 비밀번호가 일치하지않습니다.");
			}
			})
		})
	}

</div>

<div><h6>unregisterService.java</h6></div>
<div markdown="1">
		
	public class unregisterService implements Command {
	@Override
	public String execute(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
   		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();

		String u_id = request.getParameter("id");
		String u_pw = request.getParameter("pw");

		User_DTO u_DTO = new User_DTO();
		u_DTO.setId(u_id);
		u_DTO.setPw(u_pw);

		User_DAO dao = new User_DAO();
		int res = dao.unregister(u_DTO);
		
		if(res>0) {
			out.print("{\"name\":\""+res+"\"}");	
		}
		return null;
	}

	}	
    
</div>

<div><h6>User_DAO : unregister()</h6></div>
<div markdown="1">
	
		public int unregister(User_DTO dto) {
		
		SqlSession sqlSession = factory.openSession(true);
		int res = sqlSession.delete("unregister", dto);
		sqlSession.close();
		return res;
		
	}

</div>

<div><h6>Mapper.xml : id="unregister"</h6></div>
<div markdown="1">
	
	<delete id="unregister" parameterType="com.YOU_I.model.User_DTO">
		DELETE FROM TBL_USER
		WHERE
		id = #{id} AND pw = #{pw}
	</delete>

</div>
 </details>
 

</br>

#### 4. 프로젝트 후기😂
> 👩 : 프로젝트를 진행하는 동안엔 꽤나 많이 힘들었다. "왜 이렇게 안되지", "왜 이렇게 못하지" 만
       천번 되뇌였다. 하지만 고생 끝에 낙이온다고 코드를 보면서 이전에는 보이지 않던 것들이 보이 
      기 시작했다. 그간 새롭게 알게된 것들, 공부한 것들을 아래 나열해보겠다 !!
</br>

#### 5. Study
<details><summary><h5>📍 쿼리스트링이란?</h5></summary>
<div>1. 우리가 진행한 프로젝트에서는 각 그룹마다 커뮤니티 페이지가 존재했다.</div>
<div>2. 그렇다면 사용자가 커뮤니티 페이지에 접속했을 때 각 사용자에 따라 가입한 그룹의 정보만을 화면에 보여줘야 한다.</div>
<div>3. 또한, 페이지가 이동되더라도 서버측에 보내야하는 데이터의 값들이 사라지면 안됐다.</div>
<div>4. 따라서 URL의 뒤에 입력 데이터를 함께 제공하는 가장 단순한 데이터 전달 방법이자 웹개발에서 데이터를 요청하는 방식 중 주로 GET방식으로 데이터를 요청할 때 쓰이는 방법인 쿼리스트링 방식을 생각하게 됐다.</div>
<h4>"리소스?이름=값" 형식.</h4>
<div markdown="1">

    $(document).ready(function(){
        $.ajax({
            url: 'getGroupName.do?groupNo=' + GroupNo,
            dataType: 'json',
            success: function(data){
                
        })
        });

</div>
 </details>

<details><summary><h5>📍 JQuery 메서드</h5></summary>
<div><h7> $(선택자).html(); -> 선택한 요소에 하위 요소들을 반환.</h7></div>
<div><h7> $(선택자).text(); -> 선택한 요소 안에 텍스트만을 반환</h7></div> 
<div><h7> $(선택자).hide(); -> 선택한 요소를 숨기기</h7></div>
<div><h7> $(선택자).show(); -> 선택한 요소를 표시하기</h7></div>
<div><h7> $(선택자).slideToggle(); -> 숨겨져 있던 요소는 아래로 펼쳐지며 노출되고, 노출되어 있던 요소는 위로 접으면서 숨김</h7></div>
<div><h7> $(선택자).css("스타일 속성 이름", "속성 값"); -> 해당 선택자에 원하는 스타일 부여</h7></div>
<div><h7> $(선택자).attr("속성 이름", "속성 값"); -> 해당 선택자에 속성값 설정하기</h7></div>
 </details>

<details><summary><h5>📍 Gson 라이브러리</h5></summary>
<div><h7>Gson라이브러리란 Google에서 만든 Java용 라이브러리로, JSON 데이터와 Java 객체 간의 변환을 쉽게 할 수 있도록 도와주는 도구이다. 프로젝트에서 각 그룹마다 소속된 사용자들의 닉네임, 연락처, 직급 등의 정보를 객체 배열 형태로 가져오기 위해 사용했다. </h7></div> 
<p></p>
<div markdown="1">

	public class memberInfoService implements Command {
	@Override
		public String execute(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();

		request.setCharacterEncoding("utf-8");

		String groupNo = request.getParameter("groupNo");
		int groupNoInt = Integer.parseInt(groupNo);

		User_DTO dto = new User_DTO();
		dto.setGroupNo(groupNoInt);

		User_DAO dao = new User_DAO();
		List<User_DTO> res = dao.member(dto);


		if (res.isEmpty()) {
			out.print("false");
		} else {
			Gson gson = new Gson();
			String result = gson.toJson(res);
			out.print(result);
		}
		return null;
		}
	}

</div>
</details>

[![Harlok's WakaTime stats](https://github-readme-stats.vercel.app/api/wakatime?username=kangchaelin)](https://github.com/anuraghazra/github-readme-stats)
![Top Langs](https://github-readme-stats.vercel.app/api/top-langs/?username=kangchaelin&layout=compact)

