JDBC, Java Database Connectivity
- 자바 응용 프로그램(콘솔,웹,모바일 등)과 데이터베이스 관리 시스템(오라클,MySQL 등) 연결시켜주는 중간계층
- 자바 프로그램 ↔ 오라클 X
- 자바 프로그램 ↔ JDBC ↔ 오라클 O
- 중간계층 : JDBC

[사람 + SQL Deverloper ↔ Oracle Server]
- 지난 3주간 환경
1. 클라이언트 툴 실행
2. DB서버 접속
  2.1 호스트명 : 서버 IP or 도메인 주소 → localhost
  2.2 포트번호 : 1521
  2.3 SID : "xe"
  2.4 드라이버 : "thin(oci)"
  2.5 사용자명 : "hr"
  2.6 비밀번호 : "java1234"
3.질의(업무)
  3.1 SQL 사용
  3.2 반환값이 없는 쿼리
    - select를 제외한 모든 쿼리
  3.3 반환값이 있는 쿼리
    - select
    - 결과셋을 반환하는 쿼리
    - 결과셋을 업무에 사용★
  4. 접속종료
    4.1 commit/rollback
    4.2 접속 종료

  [자바프로그램 + JDBC ↔ Oracle Server]
  - 이시간 이후 환경
  1. 자바 응용 프로그램 실행
  2. DB 서버 접속
    - JDBC(Connection 클래스) 사용
    2.1 호스트명 : 서버 IP or 도메인 주소 → localhost
    2.2 포트번호 : 1521
    2.3 SID : "xe"
    2.4 드라이버 : "thin(oci)"
    2.5 사용자명 : "hr"
    2.6 비밀번호 : "java1234"
  3. 질의
    - Statement 클래스 사용
    3.1 SQL 사용
    3.2 반환값이 없는 쿼리
      - select를 제외한 모든 쿼리
    3.3 반환값이 있는 쿼리
      - select
      - 결과셋을 ResultSet클래스를 사용해서 반환(제어)
      - 결과셋을 반환하는 쿼리
      - 결과셋을 업무에 사용★
    4. 접속종료
      - Connection 클래스 사용
      4.1 commit/rollback
      4.2 접속 종료

    JDBC 관련 클래스 라이브러리
    - Connection, Statement, ResultSet 클래스

    JDBC 사용 환경 설정
    - 현재 프로젝트에서 JDBC를 사용하기 위한 설정
    - JDBC 드라이버 파일이 필요★
    - 오라클 사이트 → 다운로드
    - 구글링
    - 오라클 설치 폴더에 이미 들어있음(권장)
    - D:\app\oracle\product\11.2.0\server\jdbc\lib\ojdbc6.jar 를 자바에 lib폴더하나 만들어서 그안에 복사시키고
      프로젝트에서 우클릭 → Build Path → Configure Build Path
      → 상단 탭에서 Libraries → Add JARs → src에서 폴더 찾아서 OK → Apply and Close
      다 되면 Package Explorer창에 Referenced Libraries폴더가 생기고 그 안에 jar파일이 들어있음



ex) DBUtil클래스 하나 만들고 import com.project.ssacademy.DBUtil; 이렇게 필요한 페이지에서 import해서 사용
→ conn = DBUtil.open(); 이렇게 한다음 자동 import하기(ctrl+shift+o)

public class DBUtil {

	private static Connection conn;

	public static Connection open() {
		
		String url = "jdbc:oracle:thin:@localhost:1521:xe"; 
		
		String id = "project";
		String pw = "java1234";
		
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver");
			
			conn = DriverManager.getConnection(url, id, pw);
						
			return conn;

		} catch (Exception e) {
			System.out.println("DBUtil.open()");
			e.printStackTrace();
		}
		
		return null;
		
	}
	
	public static Connection open(String server, String id, String pw) {
		
		String url = "jdbc:oracle:thin:@" + server + ":1521:xe";
		
		try {

			Class.forName("oracle.jdbc.driver.OracleDriver");
			
			conn = DriverManager.getConnection(url, id, pw);
			
			return conn;

		} catch (Exception e) {
			System.out.println("DBUtil.open()");
			e.printStackTrace();
		}
		
		return null;
		
	}
	
}

↓↓↓↓아래는 위 코드의 해석↓↓↓↓

	public static void main(String[] args) {

//		1. DB접속
		Connection conn;

//		2. 연결 문자열(Connection String)
		String url="jdbc:oracle:thin:@localhost:1521:xe";
		String id="project2";
		String pw="java1234";

//		JDBC작업 → 외부 입출력 → 예외처리 필수
		try {
		
//			3. JDBC관련 드라이버 로딩
			Class.forName("oracle.jdbc.driver.OracleDriver");
		
//			4. Connection 객체 생성 + 오라클 접속
			conn=DriverManager.getConnection(url,id,pw);
		
//			5. 업무
			System.out.println(conn.isClosed()); //false가 나오면 연결이 되어있는것
		
//			6. 접속 종료
			conn.close();
			System.out.println(conn.isClosed()); //true가 나오면 연결이 끊긴것
		
		} catch (Exception e) {
			System.out.println("Ex01.main()");
			e.printStackTrace();
		}
		
	}



아래의 내용은 보일러플레이트(boilerplate) 코드로서, 베이스로 깔고 가는 코드임

Connection conn = null;
Statement stat = null;
ResultSet rs = null;

try {

	conn = DBUtil.open();
	stat = conn.createStatement();
	
	String sql = "";
	
	
	
	
} catch (Exception e) {
	System.out.println("Ex05_select.m3()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

ex) select 문 (executeQuery,ResultSet)

Connection conn = null;
Statement stat = null;
ResultSet rs = null;

try {
	
	conn = DBUtil.open();
	stat = conn.createStatement();
	
	String sql="select * from tblAddress order by seq asc";
	
	rs = stat.executeQuery(sql);
	
	System.out.println("[번호]\t[이름]\t[나이]\t[성별]\t[전화번호]\t\t[등록일]\t\t\t[주소]\n");
	while (rs.next()) {
		System.out.printf("%s\t%s\t%s\t%s\t%s\t%s\t%s\n",
				rs.getString("seq"),
				rs.getString("name"),
				rs.getString("age"),
				rs.getString("gender").equals("m")?"남자":"여자",
				rs.getString("tel"),
				rs.getString("regdate"),
				rs.getString("address")
		);
	}
	rs.close();
	stat.close();
	conn.close();
	
} catch (Exception e) {
	System.out.println("Ex05_select.m4()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

ex) 1개의 레코드 select

while을 if로 바꾸기

	if(rs.next()) {
		AdminDTO dto = new AdminDTO();

		dto.setTel(rs.getString("tel"));
		dto.setEmail(rs.getString("email"));

		return dto;
	}

----------------------------------------------------------------------------------------------------

ex) insert / update 문 (executeUpdate)

Connection conn = null;
Statement stat = null;

try {
	
	conn=DBUtil.open();
	
	String sql = String.format("insert into tbladdress3 (seq,name,age,gender,tel,address,regdate) values (seqaddress3.nextVal,'%s','%d','%s','%s','%s',sysdate)","김동강",24,"r","010-1234-1222","서울시");

	stat=conn.createStatement();
	
	int result = stat.executeUpdate(sql);
	
	if (result>0) {
		System.out.println("주소록 추가 성공!");
	}else {
		System.out.println("주소록 추가 실패!");
	}
	
	stat.close();
	conn.close();
	
} catch (Exception e) {
	System.out.println("test.main()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

ex) 매개변수처리한 insert / update 문 (PreparedStatement)

Connection conn = null;
PreparedStatement pstat = null;

String name = "한가인";
int age = 24;
String gender = "f";
String phone = "010-1659-4567";
String address = "경기도 고양시";

try {
	
	conn = DBUtil.open();
	
	String sql = "insert into tbladdress3 (seq,name,age,gender,tel,address,regdate) values (seqaddress3.nextVal,?,?,?,?,?,sysdate)";
	
	pstat = conn.prepareStatement(sql);
	pstat.setString(1,name);
	pstat.setInt(2,age);
	pstat.setString(3,gender);
	pstat.setString(4,phone);
	pstat.setString(5,address);
	
	return pstat.executeUpdate();
	
	pstat.close();
	conn.close();
	
} catch (Exception e) {
	System.out.println("test.main()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

ex) 검색

Scanner scanner = new Scanner(System.in);

Connection conn = null;
PreparedStatement pstat = null;
ResultSet rs = null;

try {
	
	System.out.print("검색할 주소입력 : ");
	String searchAddr = scanner.nextLine();
	searchAddr = searchAddr.replace(searchAddr,"%"+searchAddr+"%");
	
	conn = DBUtil.open();
	
	String sql = "select name,age,address from tbladdress3 where address like ?";
	
	pstat = conn.prepareStatement(sql);
	pstat.setString(1,searchAddr);
	
	rs = pstat.executeQuery();
	
	while(rs.next()) {
		System.out.printf("%s\t%s\t%s\n",
			rs.getString("name"),
			rs.getString("age"),
			rs.getString("address")
		);
	}
	
	rs.close();
	pstat.close();
	conn.close();
	
} catch (Exception e) {
	System.out.println("test.main()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

추가DAO

public static void addStudent() {
	
	ArrayList<StudentDTO> list = getStudent("");
	
	System.out.println();
	String name="";
	while (true) {
		System.out.print("\t- 이름을 입력하세요.(1/6) : ");
		name = scanner.nextLine();
		if (name.equals("")) {
			System.out.println("\t\t※ 이름은 필수값입니다. 다시 입력하세요.\n");
		}else {
			break;
		}
	}
	String id="";
	while (true) {
		System.out.print("\t- 아이디를 입력하세요.(2/6) : ");
		id = scanner.nextLine();
		if (id.equals("")) {
			System.out.println("\t\t※ 아이디는 필수값입니다. 다시 입력하세요.\n");
		}else {
			boolean result=true;
			for (int i = 0; i < list.size(); i++) {
				if (list.get(i).getId().equals(id)) {
					result=false;
					break;
				}
			}
			if (result) {
				break;
			}else {
				System.out.println("\t\t※ 중복된 아이디입니다. 다시 입력하세요.\n");
			}
		}
	}
	String ssn="";
	while (true) {
		System.out.print("\t- 주민등록번호를 입력하세요.(3/6) : ");
		ssn = scanner.nextLine();
		if (ssn.equals("")) {
			System.out.println("\t\t※ 주민등록번호는 필수값입니다. 다시 입력하세요.\n");
		}else {
			break;
		}
	}

	System.out.print("\t- 휴대폰번호를 입력하세요.(4/6) : ");
	String phone = scanner.nextLine();
	System.out.print("\t- 이메일을 입력하세요.(5/6) : ");
	String email = scanner.nextLine();
	System.out.print("\t- 희망취업분야를 입력하세요.(6/6) : ");
	String employmentField = scanner.nextLine();

	try {
		
		conn = DBUtil.open();
		
		String sql = "insert into tblStudent (seqStudent,name,id,ssn,phone,email,firstRegistrationDate,employmentField) values (seqStudent.nextVal,?,?,?,?,?,sysdate,?)";
		
		pstat = conn.prepareStatement(sql);
		pstat.setString(1,name);
		pstat.setString(2,id);
		pstat.setString(3,ssn);
		pstat.setString(4,phone);
		pstat.setString(5,email);
		pstat.setString(6,employmentField);
		
		int result = pstat.executeUpdate();
		
		System.out.println();
		pstat.close();
		conn.close();
		
		if (result==1) {
			System.out.println("\t\t※ 교육생 추가가 완료되었습니다.");
		}else {
			System.out.println("\t\t※ 교육생 추가실패");
		}
		System.out.println();
		
		return;
		
	} catch (Exception e) {
		System.out.println("test.main()");
		e.printStackTrace();
	}
	
}

----------------------------------------------------------------------------------------------------

수정

↓↓메인 DAO↓↓
public static void modStudent() {
	ArrayList<StudentDTO> list = studentList("");
	StudentDAO dao = new StudentDAO();
	StudentDTO dto = new StudentDTO();
	
	AdministerStudent.printInfoList(list); //리스트를 출력하는 메소드
	
	System.out.println();
	System.out.print("\t█ 수정하실 학생번호를 입력하세요 : ");
	String seq = scanner.nextLine();
	
	dto = dao.get(seq);
	AdministerStudent.printInfo(dto); //정보를 출력하는 메소드
	
	System.out.println();
	System.out.println("\t\t※ 수정하지 않으실 항목은 빈값으로 엔터를 입력하세요");
	
	System.out.print("\t수정할 이름을 입력하세요 : ");
	String name = scanner.nextLine();
	
	if (name.equals("")) {
		name = dto.getName();
	}
	
	String id="";
	while(true) {
		System.out.print("\t수정할 아이디를 입력하세요 : ");
		id = scanner.nextLine();
		if (id.equals("")) {
			id = dto.getId();
			break;
		}else {
			boolean result=true;
			for (int i = 0; i < list.size(); i++) {
				if (list.get(i).getId().equals(id)) {
					result=false;
					break;
				}
			}
			if (result) {
				break;
			}else {
				System.out.println("\t\t※ 중복된 아이디입니다. 다시 입력하세요.\n");
			}
		}
	}
	
	System.out.print("\t수정할 휴대폰을 입력하세요 : ");
	String phone = scanner.nextLine();
	
	if (phone.equals("")) {
		phone = dto.getPhone();
	}
	
	System.out.print("\t수정할 이메일을 입력하세요 : ");
	String email = scanner.nextLine();
	
	if (email.equals("")) {
		email = dto.getEmail();
	}
	
	System.out.print("\t수정할 가입일을 입력하세요 : ");
	String regDate = scanner.nextLine();
	
	if (regDate.equals("")) {
		regDate = dto.getFirstRegistrationDate();
	}
	
	System.out.print("\t수정할 취업희망분야를 입력하세요 : ");
	String empField = scanner.nextLine();
	
	if (empField.equals("")) {
		empField = dto.getEmploymentField();
	}
	
	StudentDTO dto2 = new StudentDTO();
	
	dto2.setSeqStudent(dto.getSeqStudent());
	dto2.setName(name);
	dto2.setId(id);
	dto2.setPhone(phone);
	dto2.setEmail(email);
	dto2.setFirstRegistrationDate(regDate);
	dto2.setEmploymentField(empField);
	
	System.out.println();
	System.out.println("\t\t※ 정보를 확인하세요.\n");
	
	System.out.printf("\t=====%s번 교육생=====",dto.getSeqStudent());
	System.out.println("\t<수정전>");
	System.out.printf(""
			+ "\t성명         : %s\n"
			+ "\t아이디       : %s\n"
			+ "\t휴대폰       : %s\n"
			+ "\t이메일       : %s\n"
			+ "\t가입일       : %s\n"
			+ "\t취업희망분야 : %s\n",
			dto.getName(),
			dto.getId(),
			dto.getPhone(),
			dto.getEmail(),
			dto.getFirstRegistrationDate(),
			dto.getEmploymentField()
	);
	System.out.println();
	System.out.println("\t\t\t▼");
	System.out.println("\t\t\t\t<수정후>");
	System.out.printf(""
			+ "\t성명         : %s\n"
			+ "\t아이디       : %s\n"
			+ "\t휴대폰       : %s\n"
			+ "\t이메일       : %s\n"
			+ "\t가입일       : %s\n"
			+ "\t취업희망분야 : %s\n",
			dto2.getName(),
			dto2.getId(),
			dto2.getPhone(),
			dto2.getEmail(),
			dto2.getFirstRegistrationDate(),
			dto2.getEmploymentField()
	);
	System.out.println();
	System.out.print("\t█ 수정하시겠습니까? (y/n) : ");
	String txt = scanner.nextLine();
	if (!txt.toUpperCase().equals("Y")) {
		System.out.println("\t취소되었습니다. 이전 메뉴로 돌아갑니다.");
		return;
	}
	
	String sql = "update tblStudent set name=?,id=?,phone=?,email=?,firstRegistrationDate=?,employmentField=? where seqStudent=?";	
	
	int result=0;
	try {
		
		pstat = conn.prepareStatement(sql);
		
		pstat.setString(1, dto2.getName());
		pstat.setString(2, dto2.getId());
		pstat.setString(3, dto2.getPhone());
		pstat.setString(4, dto2.getEmail());
		pstat.setString(5, dto2.getFirstRegistrationDate());
		pstat.setString(6, dto2.getEmploymentField());
		pstat.setString(7, dto2.getSeqStudent());
		
		result = pstat.executeUpdate();
		
		pstat.close();
		
	} catch (Exception e) {
		System.out.println("StudentDAO.modStudent()");
		e.printStackTrace();
	}
	
	System.out.println();
	if (result > 0) {
		System.out.println("\t\t※ 정보 수정이 완료되었습니다.");
	} else {
		System.out.println("\t\t※ 정보 수정에 실패했습니다.");
	} 
	System.out.println();
	
	return;
	
}

↓↓교육생 정보 받는 DAO↓↓
public StudentDTO get(String seq) {
	
	
	try {
		
		conn=DBUtil.open();
		stat=conn.createStatement();

		String sql = "select * from tblStudent where seqStudent = ?";
		
		pstat = conn.prepareStatement(sql);
		pstat.setString(1, seq);
		
		rs = pstat.executeQuery();
		
		if (rs.next()) {
			StudentDTO dto = new StudentDTO();
			
			dto.setSeqStudent(rs.getString("seqStudent"));
			dto.setName(rs.getString("name"));
			dto.setId(rs.getString("id"));
			dto.setPhone(rs.getString("phone"));
			dto.setEmail(rs.getString("email"));
			dto.setFirstRegistrationDate(rs.getString("firstRegistrationDate"));
			dto.setEmploymentField(rs.getString("employmentField"));
			
			return dto;
		}
		

	} catch (Exception e) {
		System.out.println("AddressDAO.get()");
		e.printStackTrace();
	}
	
	return null;
}

↓↓DTO↓↓
public class StudentDTO {

	private String seqStudent; //교육생번호
	private String name; //교육생이름
	private String id; //교육생아이디
	private String ssn; //교육생주민번호
	private String phone; //교육생전화번호
	private String email; //교육생이메일
	private String firstRegistrationDate; //교육생최초등록일
	private String employmentField; //교육생취업분야
	public int num;
	
	public String getSeqStudent() {
		return seqStudent;
	}
	public void setSeqStudent(String seqStudent) {
		this.seqStudent = seqStudent;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	public String getSsn() {
		return ssn;
	}
	public void setSsn(String ssn) {
		this.ssn = ssn;
	}
	public String getPhone() {
		return phone;
	}
	public void setPhone(String phone) {
		this.phone = phone;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getFirstRegistrationDate() {
		if (firstRegistrationDate!=null) {
			return firstRegistrationDate.substring(0,10);
		}else {
			return firstRegistrationDate;
		}
	}
	public void setFirstRegistrationDate(String firstRegistrationDate) {
		this.firstRegistrationDate = firstRegistrationDate;
	}
	public String getEmploymentField() {
		return employmentField;
	}
	public void setEmploymentField(String employmentField) {
		this.employmentField = employmentField;
	}
	
}

----------------------------------------------------------------------------------------------------

삭제

↓↓메인↓↓
private static void st_remove() { //교육생 정보 삭제
	
	ArrayList<StudentDTO> list = dao.studentList(null);
	
	for (StudentDTO dto : list) {
		System.out.printf("%s - %s\n", dto.getSeqStudent(), dto.getName());
	}
	System.out.println();
	
	System.out.print("삭제할 직원 번호: ");
	String seq = scanner.nextLine();
	
	int result = dao.removeStudent(seq);
	
	if (result > 0) {
		System.out.println("주소록 삭제 성공");
	} else {
		System.out.println("주소록 삭제 실패");
	}
	
	AdministerStudent(sadto);
}

↓↓삭제하는 DAO↓↓
public int removeStudent(String seq) {

	try {

		String sql = "delete from tblStudent where seqStudent = ?";
		
		pstat = conn.prepareStatement(sql);
		pstat.setString(1, seq);
		
		return pstat.executeUpdate(); // 1 or 0

	} catch (Exception e) {
		System.out.println("StudentDAO.delete()");
		e.printStackTrace();
	}
	
	return 0;
}

----------------------------------------------------------------------------------------------------

ex) 기본 프로시저 호출

Connection conn = null;
CallableStatement cstat = null;

try {

	conn = DBUtil.open();
	
	String sql = "{ call procM1 }";
	
	cstat = conn.prepareCall(sql);
	
	int result = cstat.executeUpdate();
	
	System.out.println(result);
	System.out.println("완료");
	

} catch (Exception e) {
	System.out.println("Ex07_CallableStatement.m1()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

ex) 인자값(O), 반환값(X) 프로시저 호출

Connection conn = null;
CallableStatement stat = null;

try {

	conn = DBUtil.open();
	
	String sql = "{ call procM2(?, ?, ?, ?, ?) }";
	
	//String sql = String.format("{ call procM2('%s', %s, '%s', '%s', '%s') }", "", 1, "", "" ,"");
	
	stat = conn.prepareCall(sql);
	
	stat.setString(1, "하하하");
	//stat.setString(2, "20");
	stat.setInt(2, 20);
	stat.setString(3, "f");
	stat.setString(4, "010-1234-5677");
	stat.setString(5, "서울시 강동구 길동");
	
	
	System.out.println(stat.executeUpdate());
	
	System.out.println("완료");
	
	stat.close();
	conn.close();
	
	

} catch (Exception e) {
	System.out.println("Ex07_CallableStatement.m2()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

ex) 인자값(X), 반환값(O) 프로시저 호출

Connection conn = null;
CallableStatement stat = null;
//ResultSet rs;

try {

	conn = DBUtil.open();
	
	String sql = "{ call procM3(?) }";
	
	stat = conn.prepareCall(sql);
	
	//in 매개변수X
	//stat.setXXX(1, 값);
	
	//out 매개변수O
	stat.registerOutParameter(1, OracleTypes.NUMBER);
	
	//ResultSet rs = stat.executeQuery();
	//System.out.println(rs.next());
	
	stat.executeQuery();
	
	int count = stat.getInt(1);
	System.out.println("주소록 항목: " + count);
	
	stat.close();
	conn.close();
	
	

} catch (Exception e) {
	System.out.println("Ex07_CallableStatement.m3()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

ex) 프로시저가 반환한 커서 참조하기

Connection conn = null;
CallableStatement stat = null;

try {

	conn = DBUtil.open();
	
	String sql = "{ call procM5(?,?) }";
	
	stat = conn.prepareCall(sql);
	
	stat.setString(1, "개발부");
	stat.registerOutParameter(2, OracleTypes.CURSOR);
	
	stat.executeQuery();
	
	//Oracle(cursor) -> JDBC(ResultSet)
	ResultSet rs = (ResultSet)stat.getObject(2);
	
	while (rs.next()) {
		System.out.println(rs.getString("name"));
		System.out.println(rs.getString("jikwi"));
		System.out.println(rs.getString("city"));
		System.out.println();
	}
	
	rs.close();
	stat.close();
	conn.close();
	
	

} catch (Exception e) {
	System.out.println("Ex07_CallableStatement.m5()");
	e.printStackTrace();
}

----------------------------------------------------------------------------------------------------

★Statement 클래스
  - SQL 구문을 실행해주는 역할(대리자)
  - 모든 SQL을 실행할 수 있다


★Statement 클래스 종류

1. Statement
  - 기본 클래스
  - 매개변수가 없는 SQL (정적 쿼리)

2. PreparedStatement
  - Statement 계량 클래스
  - 매개변수가 있는 SQL (동적 쿼리)
  - 안정성 높음 + 가독성 높음
  - 코드량 많음

3. CallableStatement
  - Statement 계량 클래스
  - 프로시저 호출 전용
  - PreparedStatement와 유사

★JDBC에서는 문장 마지막에 ;(세미콜론)을 찍으면 안됨 에러남 (ORA-00911: invalid character)
★--주석도 금지
★JDBC에서 작업하다가 중간에 sql디벨로퍼에서 수정하는경우 수정이 끝나고 다시 JDBC에서 작업하기전 반영을위해 commit 필수
★JDBC에서 작업한내용은 rollback불가
★JDBC에서 executeUpdate로 DDL 실행시 'n행이 삭제되었습니다' 이런 int반환값이 없음
★클로즈 닫혀있으면 오류 주의 (에러메세지에 '~~종료' 라고 뜸)

----------------------------------------------------------------------------------------------------

JDBC는 기본적으로 모든 쿼리의 실행시 자동 커밋이 된다
execute() → commit 호출

커밋을 끄려면 먼저 아래 구문을 추가한후
conn.setAutoCommit(false); //이 구문은 stat를 만들기 전에 호출해야 한다.
그리고 실행 후 conn.rollback();을 추가

트랜잭션 업무 처리방법
1. 오라클에서 처리 → 권장 (먼저 일어나는곳에서 먼저 처리하는게 좋음)
2. 자바(JDBC)에서 처리

----------------------------------------------------------------------------------------------------

부적합한 Oracle URL이 지정되었습니다
→ 아래 url부분이 오타났을때
String url="jdbc:oracle:thi:@localhost:1521:xe";

java.sql.SQLException: ORA-01017: invalid username/password; logon denied
→ 아래 id나 password부분이 오타났을때
String id="hr";
String pw="java1234";

java.lang.ClassNotFoundException: orace.jdbc.driver.OracleDriver
→ 아래 JDBC관련 드라이버 로딩 부분이 오타났을때

java.sql.SQLRecoverableException: IO 오류: The Network Adapter could not establish the connection
java.net.ConnectException: Connection timed out: connect
→ @뒤부분 주소로 연결불가할때
String url="jdbc:oracle:thin:@211.63.89.55:1521:xe";

Listener refused the connection with the following error:
ORA-12505, TNS:listener does not currently know of SID given in connect descriptor
→ 오라클 실행이 중지되어있을때

java.lang.NullPointerException
→ DBUtil.open()을 안열었을때
→ rs=stat.executeQuery(sql); 쿼리실행을 안했을때
→ 등등 변수가 null일때

java.sql.SQLSyntaxErrorException: ORA-00904: "NME": invalid identifier
→ sql 컬럼이름 틀렸을때

java.sql.SQLSyntaxErrorException: ORA-00942: table or view does not exist
→ sql 테이블이름 틀렸을때

java.sql.SQLSyntaxErrorException: ORA-00911: invalid character
→ sql문뒤에 ;(세미콜론) 붙였을떄

java.sql.SQLException: 부적합한 열 이름
→ getNString부분(자바로결과셋받는부분) 컬럼명 틀렸을때

java.sql.SQLSyntaxErrorException: ORA-00917: missing comma
→ 매개변수에 '(홑따옴표) 들어갔을떄
→ 직접 ''(홑따옴표두개) 붙이거나 replace("'","''") 쓰거나 preparedStatement 사용

java.sql.SQLException: 인덱스에서 누락된 IN 또는 OUT 매개변수:: 1
→ 1번째 매개변수에 값이 없을때

AddressDAO.list()
java.sql.SQLRecoverableException: 접속 종료
→ close로 잘못 닫았을때 ex)conn , stat , rs 등

----------------------------------------------------------------------------------------------------

arraylist로 담아서 저장/호출

↓↓↓저장하는 메소드↓↓↓
public ArrayList<StudentDTO> studentList(String word) {
	
	try {

		String where = "";
		
		if (word != null) {
			where = String.format("where address like '%%%s%%'", word);
		}
		
		String sql = String.format("select * from tblStudent %s order by seqStudent desc", where);
		
		rs = stat.executeQuery(sql);
		
		ArrayList<StudentDTO> list = new ArrayList<StudentDTO>();
		
		while (rs.next()) {
			StudentDTO dto = new StudentDTO();
			
			dto.setSeqStudent(rs.getString("seqStudent"));
			dto.setName(rs.getString("name"));
			dto.setId(rs.getString("id"));
			dto.setSsn(rs.getString("ssn"));
			dto.setPhone(rs.getString("phone"));
			dto.setEmail(rs.getString("email"));
			dto.setFirstRegistrationDate(rs.getString("firstRegistrationDate"));
			dto.setEmploymentField(rs.getString("employmentField"));
			
			list.add(dto);				
		}
		
		return list;

	} catch (Exception e) {
		System.out.println("AddressDAO.list()");
		e.printStackTrace();
	}
	
	return null;
}

↓↓↓불러오는 부분

ArrayList<StudentDTO> list = dao.studentList(null);
이후
호출부

----------------------------------------------------------------------------------------------------

" inner join tblStudent st on st.seqStudent=r.seqStudent" +
" order by tos.seqTopStudent";

이런 줄바꿈부분에서
" inner join tblStudent st on st.seqStudent=r.seqStudent" +
"order by tos.seqTopStudent";

↑

위처럼 사이에 공백이 없으면 ORA-00933 오류난다

----------------------------------------------------------------------------------------------------










