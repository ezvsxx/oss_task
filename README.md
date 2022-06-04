# 【 𝐋𝐈𝐍𝐔𝐗 𝐂𝐎𝐌𝐌𝐀𝐍𝐃𝐒 : 𝐏𝐒, 𝐓𝐎𝐏, 𝐊𝐈𝐋𝐋, 𝐉𝐎𝐁𝐒 】

####  **<프로세스 관련 기본 용어>**

|용어|내용|
|---|---|
|**프로세스(process)**| 현재 시스템에서 실행 중인 프로그램|
|**PID**|각 프로세스는 고유한 번호|
|**포그라운드 (forground)**|입력한 명령어 실행이 결과가 나올 때 까지 기다리는 방식|
|**백그라운드(background)**|하나의 쉘에서 여러 개의 프로세스를 동시에 실행할 수 있는 방식|
|**멀티 태스킹 (multi-tasking)**|동시에 여러 명령어들을 실행시키는 것|
|**시그널(signal)**|프로세스끼리 통신할 때 사용하는 신호|
|**인터럽트 시그널(interupt signal)**|리눅스 사용자 입력에 의한 시그널|


## ◈ 𝐏𝐒
- 현재 실행 중인 프로세스를 출력하는 명령어


### <code>▸ option</code>
|옵션|내용|
|:---:|:---:|
|**-e**|시스템상의 모든 프로세스에 대한 정보 출력|
|**-u**|프로세스 소유자 정보를 함께 출력 |
|**-f**|전체 포맷으로 출력|

### <code>▸ examples</code>

~~~blackquote
ps [옵션]
$ ps -ef | more         : 모든 프로세스를 full format으로 출력하고 페이지 단위로 출력
$ ps -ef | grep apache  : grep을 이용하여 apache가 포함된 모든 라인 출력
$ ps -fp [PID]           pid를 키워드로 프로세스 정보를 확인
~~~

## ◈ 𝐓𝐎𝐏  
- 시스템 프로세스/메모리 사용 현황을 <code>실시간</code>으로 출력하는 명령어
- 윈도우의 작업관리자와 유사함

### <code>▸ option</code>
|옵션|내용|
|:---:|:---:|
|**P**|CPU 사용률 내림차순|
|**M**|메모리 사용률 내림차순|
|**t**|실행된 시간이 큰 순서로 정렬|
|**k**|프로세스 종료|
|**q**|	top명령 종료|
|**-f**|전체 포맷으로 출력|
|**n**|	출력한 프로세스 개수 바꿈|
### <code>▸ examples</code>
```
top [옵션] 
$ top -n 5           : 실행 주기 설정(3초단위로 5회 실행)
$ top -p 13127       : pid 13127 프로세스만 묘시
$ top | grep “name”  : grep을 이용하여 원하는 프로세스만 보기
```

## ◈ 𝐊𝐈𝐋𝐋 
- 대게 프로세스를 죽일 때 사용하는 명령어
- 원래 내부적으로는 프로세스에 특정 <code>시그널</code>을 보내는 명령어

### <code>▸ signal list</code>

|번호|시그널|내용|
|---|---|---|
|1|**SIGHUP**|터미널 접속이 끊겼을 때 보내지는 시그널|
|2|**SIGINT**|키보드로 오는 인터럽트 시그널로 **Ctrl+c** 입력시 보내짐|
|3|**SIGQUIT**| 실행 중지 시그널로서 **Ctrl+\\** 입력시 보내짐|
|9|**SIGKILL**|프로세스를 강제로 종료 시키는 시그널|
|15|**SIGTERM)**| 프로그램을 종료하는 일반적인 방법으로 정상 종료 시키는 시그널 |
|18|**SIGCONT**| 시그널에 의해 정지된 프로세스를 다시 실행시키는 시그널|
|19|**SIGTOP**|정지시그널. SIGSTP와 같으나 잡거나 무시할 수 없음|
|20|**SIGTSTP**|일시정지 시키는 시그널로 **Ctrl+z**입력시 보내짐|

### <code>▸ examples</code>
```
kill [옵션 or 시그널(번호 or 이름)] PID
& kill 12345          : PID가 12345인 프로세스 종료
$ kill -9 1234        : ID가 12345인 프로세스 강제 종료
$ kill -SIGKILL 1234  : ID가 12345인 프로세스 강제 종료(SIGKILL = -9)
$ kill -l             : kill 명령어에서 지원하는 시그널 목록 출력
```

## ◈ 𝐉𝐎𝐁𝐒 
- 작업이 중지된 상태, 백그라운드로 진행 중인 상태, 변경 되었지만 보고 되지 않은 상태 등을 표시하는 명령어 


### <code>▸ option</code>

|옵션|내용|
|:---:|:---:|
|**-l**|프로세스 그룹 ID를 state 필드 앞에 출력|
|**-n**|프로세스 그룹 중에 대표 프로세스 ID를 출력|
|**-p**|각 프로세스 ID에 대해 한 행씩 출력|
|**command**| 지정한 명령어 실행|

### <code>▸ stats</code>

|옵션|내용|
|---|---|
|**Running**|작업이 종료하지 않고 계속 진행 중력|
|**Done**|작업이 완료되어 0을 반환하고 종료 함|
|**Stopped**|작업이 일시 중단|
|**Doen(code)**|작업이 정상적 완료 코드를 반환|
|**Stopped(SIGTSTP)**|SIGTSTP 신호가 작업을 일시 중단|
|**Stopped(SIGSTOP)**|SIGSTOP 신호가 작업을 일시 중단|
|**Stopped(SIGTTIN)**|SIGTTIN 신호가 작업을 일시 중단력|
|**Stopped(SIGTTOU)**|SIGTTOU 신호가 작업을 일시 중단|


# 【 𝐕𝐈𝐌 𝐌𝐀𝐂𝐑𝐎 】

## ◈ 매크로란?
- 특정한 움직임 또는 키 입력을 레지스터에에 저장함으로서 다시 실행 할 수 있는 것을 말한다.
- 단순하면서 반복되는 동작을 쉽고 빠르게 해주는 장점이 있다.



## ◈ 매크로 사용법

#### <code>▸ 매크로 기록</code>

|순서|입력|내용|
|:-:|:---:|:---|
|1|**q + 알파벳**|선택한 알파벳에 기록 시작|
|2|**원하는 동작**|반복을 원하는 동작 입력|
|3|**q**|기록 종료|

#### <code>▸ 매크로 실행</code>

|입력|내용|
|:---|:---|
|**a + 알파벳**|1회 실행|
|**@@**|방금 실행한 매크로 실행|
|**10@a**|매크로 10회 실행|

#### <code>▸ 증가 감소 매크로</code>
|입력|방법|
|---|:---|
|**CTRL + a**|	증가시키고 싶은 숫자에 커서를 두고 CTRL + a를 누름|
|**CTRL + x**|	감소시키고 싶은 숫자에 커서를 두고 CTRL + x를 누름|

#### <code>▸ 매크로 저장</code>
|기능|방법|
|---|:---|
|	**파일 열기**|:e ~/.vimrc|	
|**입력모드**| i입력|
|**저장**|let @(매크로key) = '(Ctrl+r Ctrl+r (매크로key))'|
|**종료**|:wq! 또는 x|
