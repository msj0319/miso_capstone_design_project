## MISO:) Chat App
### Capstone Design(Graduate Project) at Sangmyung University 2020

### Project Members
DEPT | ROLE | NAME
--- | --- | ---
CS | Project Leader, Android Development | [문승재](https://github.com/msj0319 "@msj0319")
CS | Android Development | [강지훈](https://github.com/kkangjee "@kkangjee")
CS | Requirements planning, Android Development| [박형찬](https://github.com/vkzlcks "@vkzlcks")
CS | Designer | [이우진]()
CS | Android Development | [이호진](https://github.com/roycmlhj "@roycmlhj")

### Use Configuration management tools
- [GitHub](https://github.com/msj0319/miso_capstone_design_project "캡스톤디자인 프로젝트 Repository")
### Use Collaboration tools
- Slack
### Use IDE, Language, API, Database
[<img src = "https://user-images.githubusercontent.com/40822689/93378700-cc539000-f897-11ea-9a38-dff2878bd19e.png" width="69px">](https://developer.android.com/studio?hl=ko "안드로이드 스튜디오") [<img src = "https://user-images.githubusercontent.com/40822689/93379498-dde96780-f898-11ea-8bdd-0ceb98c99e44.png" width="69px">](https://kotlinlang.org/ "코틀린") [<img src = "https://user-images.githubusercontent.com/40822689/93382537-33c00e80-f89d-11ea-80a4-6dab94d17088.png" width="69px" height="69px">](https://firebase.google.cn/docs/auth/android/start?hl=ko "Firebase Authentication") [<img src = "https://user-images.githubusercontent.com/40822689/93382356-fb203500-f89c-11ea-95f9-56b3459d083d.png" width="69px" height="69px">](https://firebase.google.cn/docs/database/android/start?hl=ko "Firebase Realtime Database")

### History
  - **2020/04/18**
     - firebase 플랫폼의 real-time database 종속항목을 추가.

   - **2020/05/22**
     - BottomNavigationBar(메인 화면) 구현

   - **2020/05/25**
     - Firebase로 회원 가입(추가), 삭제, 로그아웃
     - 회원 정보 : FirebaseDatabase (uid, email, emailVerified, department) 회원 가입 시 추가

   - **2020/07/21** 
     - 패키지 명 통일
     - Android Firebase Codelab Grow Friendly Chat

   - **2020/07/23** 
     - 채팅 기능 프로젝트에 Migration
     - Fragment 간 액티비티 전환 구현</br>
     - 채팅 시 자신 uid 값 Firebase에 저장 (추후 상대방 uid와 비교)
     - Notification 기능 구현

   - **2020/07/26** 
     - ~~Apache License 2.0 출처 명시~~
     - Main2Activity - 로그인 화면배치, 기능 변경
     - 회원정보 한글로 변경
     - 태그 목록 ScrollView로 구현하여 조작성 확보
     - 기능 테스트 버튼 정렬 (형찬이가 구현한 Alarm 기능 버튼 이름 부여)
     - 학과에 맞는 프로필 사진 추가
     - 65 Line, mappingDepartmentToProfileImage() 함수 구현
     - 학과 이름을 DB에서 가져오면 프로필 사진을 학과에 맞게 수정
       - 컴퓨터과학전공, 생명공학전공, 휴먼지능정보공학전공, 음악학부 일때만 적용.
       - 그 외 전공일 시 기본 프로필 사진 적용 (2020.07.26) 
       - ChatActivity의 messengerImageView(채팅 프로필사진)도 동일한 기능으로 구현 예정

   - **2020/08/26 ~ 08/28**
     - 학과 별 매칭 Database 구조화 (1:1 채팅방 만들기)
      - '과'끼리 버튼을 눌렀을 때
        - 처음 대기하는 사람이라면 deptMap-학과명-uid로 우선 저장
        - 만약 누가 대기하고 있다면 자신의 uid와 대기하는 사람의 uid를 Map에 담아 room 생성 후 채팅
        - 학과명 내의 uid값은 null값으로 초기화하여 비운다.
     - 전체 학과 별 매칭 Database 구조화 (1:1 채팅방 만들기)
        - 처음 대기하는 사람이라면 deptMap-전체학과-uid로 우선 저장
        - 만약 누가 대기하고 있다면 자신의 uid와 대기하는 사람의 uid를 Map에 담아 room 생성 후 채팅
        - 전체 학과 내의 uid값도 null값으로 초기화
    - ChatActivity 내에 ChatFragment 적용

   - **2020/08/29**
     - RandomChatFragment
        - 아무도 없이 먼저 매칭을 눌렀을 때 채팅 방으로 안들어가지는 버그 수정
     - SettingFragment
        - 사용자 정보 및 설정 페이지 구현 (기존 UI 변경, 대표색 배경)
        - 사용자 로그아웃 기능 구현
        - 사용자 삭제 기능 구현 
        - 학번, 비밀번호 입력하는 재인증 과정 후 계정 삭제
        - Firebase, Authentication, Databse 전부 데이터 삭제 확인 완료

   - **2020/08/31**
     - 과끼리 채팅 테스트
       - A user가 채팅방에 최초 진입 -> DB deptMap에 (학과 : A uid) 형태로 push, SplashActivity가 해당 roomid와 함께 출력 (Toast : roomid)
       - B user가 다음 채팅방에 진입 -> deptMap의 이미 대기해있던 같은 학과 A의 uid값이 pop
       - rooms - roomid - users - uid : department 값으로 저장 됨
       - A는 SplashActivity에서 ChatActivity로 진입 -> B는 바로 ChatActivity로 진입 함. (Toast : 사용자 2 입장)
     - ChatActivity toolbar 사용, 우측 버튼으로 방 나가기, 상대방 신고 버튼 세팅.
     - 학번, 비밀번호 미입력 하고 탈퇴하기 버튼 눌렀을 때 앱 종료 이슈 수정
     - 자잘한 nullable 변수 변경

   - **2020/09/03**
     - ChatActitivy, SplashActivity 순서 정렬
     - 이메일 인증이 안 됐음에도 Auth는 들어가 기존회원이라 인식하는 문제 해결
     - 채팅 중 매칭 종료 기능 구현
       - ~~ISSUE#19 ChatActivity 매칭 종료 시 다른 roomid를 가진 사용자의 방과 randomRoomId가 초기화 되는 현상.~~
       - ~~ISSUE#20 ChatFragment 진입시 앱이 종료되는 현상( activity에서 fragment로 보내는 bundle때문에 일어나는 것으로 확인)~~
       - ~~ISSUE#14 SplashActivity Issue.~~

   - **2020/09/07**
     - 채팅 방 나가기 구현 완료
       - splashactivity- 뒤로가기 종료 시 서버에 있는 채팅 관련 정보 삭제, 개인 randomroomid 삭제
     - ISSUE #24 RecyclerView issue
       - 현재 ChatFragment에서 메시지를 보낼 때 본인 및 상대방의 recyclerview에 반영이 안되는 issue
         => recyclerview 생성에 관한 문제
     - FCM 푸시 알람 테스트

   - **2020/09/10 ~ 11**
     - 채팅 방에 입력한 메시지 띄우기 기능 구현
     - TagsFragment 기능 개발 시작
     - FCM 푸시 알람 기능 개발

   - **2020/09/14**
     - 채팅 방 메시지 띄우기 기능 구현 완료 (상대방 메시지, 자신의 메시지 구분짓기 해야함)
     - TagsFragment 기능 구현 중, 태그 추가, DB 저장, 조회, 삭제 기능
     - 채팅 방 입장 후 앱을 백그라운드에 놓고, 상대방이 매칭 되면 푸시 알람으로 상대방의 입장 여부 알림 구현
   
   - **2020/09/15**
     - 상대방, 사용자 메시지 구분 - 채팅 기능 구현 완료.
     - SelectTags_signup : 기능 개발 중(20/09/16 ~) - 
       - 회원 가입 추가, SelectTagActivity(관심있는 태그를 계정 생성 시 추가하여 추후 태그 별 채팅이 가능하도록 함)
       - AppName 변경 : capstone_design_projrct -> 미소:)
       - 약간의 UI 개선 작업 (signup과정)
       - 서버에서 불러온 태그 리스트 당겨서 스와이프 시 정보 업데이트 가능.
       - [_#33 SelectTagActivity에서 태그 선택 후 회원가입 완료 시 user 객체에 태그 정보가 들어가지 않고 DB에 저장되는 현상_](https://github.com/msj0319/miso_capstone_design_project/issues/33 "ISSUE #33")
     - 채팅화면에서 뒤로가기 누를 시 자동으로 방 나가기 기능
     - 캡스톤 심사 준비로 인한 개발 일시 중단. (9/22)
