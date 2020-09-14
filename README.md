# 2020_1

아무것도 모르면서 용감하게 만든 첫 프로젝트 리눅스 기반 공유형 다이어리
아이템은 맨날 올라오는 과제제출일이나 시험시간을 다이어리에 매번 적어넣는게 귀찮아서 교수님이 
올리시면 내 다이어리에 자동으로 올라왔으면 좋겠다는 생각에서 시작됨

교수가 일정을 올리면 학생의 다이어리에 자동으로 업데이트되는 형식
공유하는 과목 일정과 비밀번호 리스트들은 서버에 저장하고 개인일정은 클라이언트에 저장시킨다.  
첫 프로젝트지만 막상 하니 욕심이 생겨서 보안적으로 아무 의미 없다는 것도 알지만 나름 비밀번호입력하고 인증하는 것도 만듬
또 나름 교수님도 (서버의)본인 과목에만 접근할 수 있도록 함
-> 서버에 비밀번호리스트와 접근 가능 과목 리스트를 넣어놓고 사용자가 입력하면 대조해서 확인하는 형식
(리스트는 .txt형식으로 관리자가 직접 만들어야함..ㅎㅎ)

client_db.c, server_db.c 는 파일을 읽고 쓰고 삭제하는 등등의 api를 담음
server_ac.c 는 사용자가 비밀번호를 입력하거나 과목 인증할 때 사용하는 api를 담음
client_fuc.c 는 기본 다이어리 기능을 수행할 수 있게 함

====================================================================================
내가 맡은 역할은 파일 관련 api와 사용자 인증 api (즉, _db.c 와 server_ac.c)이 주된 역할
- 음... 올린 파일은 인증까지는 되는데 인증하고 나면 좀 파일 전송 되는 듯하다가 segmentation default가 뜬다.
다이어리 기능만 진행하면 기능은 수행된다는데 내 생각엔 아무래도 api에 대한 업데이트가   
잘 공유가 안되어 생긴 문제일 것같다. 자꾸 수정하면 혼란오는 걸 자꾸 수정한 느낌? 다른 부분을 고쳤어야 했는데 ..

====================================================================================
## _db.c 의 api
- char* readFile(FILE* filename, int num) // 파일을 읽어서 한 줄씩 반환하는 api
- FILE* openreadFile(char* filename) // 읽기 파일을 여는 api
- FILE* openwriteFile(char* filename) // 쓰기 파일을 여는 api
- void writeFile(FILE* filename, char* msg) // 파일에 내용을 쓰는 api
- void deleteFile(FILE* filename, char* msg) //파일을 삭제하는 함수

## ac.c의 api
- char* decideMode(int mode) //클라이언트의 모드(교수 or 학생)를 확인
- Char* checkID(char* modefile, char* id) //인증번호(ID)를 확인
- Char* checkClient(char* msg) //클라이언트에게 인증 결과를 보냄

