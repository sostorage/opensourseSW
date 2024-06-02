# 오픈소스SW개론 과제2
리눅스 명령어 중에서 top, ps, jobs, kill 명령어에 대해 조사

top
-------------
top: 시스템의 상태를 전반적으로 가장 빠르게 파악 가능(CPU, Memory, Process)   
옵션 없이 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌

* top 실행 전 옵션
```
순간의 정보를 확인하려면 -b 옵션 추가(batch 모드)   
-n : top 실행 주기 설정(반복 횟수)   
```

* top 실행 후 명령어
```
shift + p : CPU 사용률 내림차순   
shit + m : 메모리 사용률 내림차순   
shift + t : 프로세스가 돌아가고 있는 시간 순   
k : kill. k 입력 후 PID 번호 작성. signal은 9    
f : sort field 선택 화면 -> q 누르면 RES순으로 정렬    
a : 메모리 사용량에 따라 정렬   
b : Batch 모드로 작동   
1 : CPU Core별로 사용량 보여줌    
```

* ps와 top의 차이점            
ps는 ps한 시점에 proc에서 검색한 cpu 사용량    
top은 proc에서 일정 주기로 합산해 cpu 사용률 출력   

ps
-------------
ps: 현재 실행중인 프로세스의 목록을 보는 명령어

* ps 옵션
```
-e(= -A): 실행중인 모든 프로세스의 정보를 출력    
-a: 세션 리더와 터미널과 연관되지 않은 프로세스를 제외하고 모든 프로세스 출력   
-C: 지정한 프로세스의 실행 파일 이름의 정보만 출력    
-u [사용자이름]: 특정 사용자에 대한 모든 프로세스의 정보를 출력, 다른 옵션도 함께 사용 가능    
-f: 프로세스에 대한 자세한 정보를 출력 (PPID 확인 가능)   
   -f 옵션들의 항목:      
    UID: 프로세스를 실행한 사용자 ID   
    PID: 프로세스 번호    
    PPID: 부모 프로세스 번호    
    C: CPU 사용량(%값)     
    STIME: 프로세스의 시작 시간      
    TTY: 프로세스가 실행된 터미널의 종류와 번호    
    TIME: 프로세스 실행 시간(실행되기 전에는 0)       
    CMD: 이런 명령어를 사용했다.       
p: 지정한 PID의 목록 정보를 출력     
l: BSD 형식의 긴 형식으로 출력      
e: 프로세스 정보와 함께 프로세스의 환경변수 정보도 출력   
-l: 긴 포맷으로 출력     
-o: 사용자 정의 형식 지정 가능      
u: 프로세스의 소유자의 이름, CPU 사용량, 메모리 사용량 등 상세 정보를 출력    
a: 터미널에서 연관된 프로세스의 정보를 출력           
   STAT(프로세스의 상태를 나타냄. R(실행중), S(인터럽트 가능한 대기(sleep) 상태), T(작업 제어에 의해 정지된(stopped) 상태), Z(좀비프로세스))            
x: 터미널과 연관되지 않는 프로세스의 정보를 출력        
=> 대부분 **ps aux** 로 씀          
```

* ps 명령어와 각종 옵션의 상세                 
1. ps 명령을 옵션없이 사용하면 현재 셀이나 터미널에서 실행한 사용자 프로세스에 대한 정보를 출력한다. (일시적인) PID는 프로세스 번호, TTY는 터미널 번호, TIME은 해당 프로세스가 사용한 CPU 시간의 양, CMD는 프로세스가 실행중인 명령이 무엇인지 알려준다.          
2. tar 명령을 이용하여 명령을 실행하고 ps 명령어로 time이 올라가는 것을 확인 가능하다.       

* ps 명령어의 장단점              
장점: 모든 프로세스 목록을 확인할 수 있고, 자세한 정보를 제공한다.             
단점: 작업 목록을 확인하기 위해서는 옵션을 추가로 지정해야 하며, 백그라운드에서 실행 중인 프로세스를 확인하기 어렵다.        

jobs
-------------
jobs: 셸에서 실행중인 프로세스 목록을 확인할 수 있는 명령어         

```
jobs [OPTIONS] [JOB]             
jobs 명령어는 옵션이나 인자 없이 주로 사용. 단, 실행중인 작업이 없다면 아무것도 출력되지 않는다.    
```   

* jobs 명령어 옵션         
```
-l 옵션: 프로세스 ID와 함께 잡 목록을 출력         
-n 옵션: 마지막로 알림 이후 변경된 잡만 출력        
-p 옵션: 잡의 프로세스 ID만 출력       
-r 옵션: 실행 중인 잡만 출력         
-s 옵션: 중지된 잡만 출력          
```

* ps 명령어와 jobs 명령어의 차이점             
ps 명령어는 모든 프로세스의 목록을 보여주며, 사용자가 실행한 프로세스 또는 시스템 프로세스를 모두 포함한다. 반면에 jobs 명령어는 현재 쉘 세션에서 실행 중인 프로세스 목록만을 보여준다. 따라서 백그라운드에서 실행 중인 프로세스를 확인하려면 jobs 명령어를 사용해야한다.          
또한, ps 명령어는 더 자세한 정보를 제공하며, 필요한 옵션을 사용하여 원하는 결과를 얻을 수 있다. 반면에 jobs 명령어는 현재 프로세스의 상태만을 간단하게 보여주는 목적으로 사용된다.        

* jobs 명령어의 장단점           
장점: 현재 쉘 세션에서 실행 중인 작업 목록을 간단하게 확인할 수 있다.            
단점: 백그라운드에서 실행 중인 다른 쉘 세션의 작업 목록을 확인할 수 없으며, 자세한 정보를 제공하지 않는다.           

kill
-------------
kill: 실행중인 리눅스 프로세스를확인하고 종료하는 명령어 

```
kill [옵션] <PID>
```

* kill 명령어 옵션
```
-s <signal>: 특정 시그널(signal)을 사용하여 프로세스를 종료. 기본적으로 SIGTERM 시그널이 사용된다.      
-l, --list: 지원되는 시그널(signal) 목록을 출력      
-a, --all: 현재 사용자에 속한 모든 프로세스를 종료        
-q, --queue: 프로세스에 시그널을 보내는 대신 시그널을 대기열에 추가                 
-9 <PID>: SIGKILL 시그널을 사용하여 강제로 프로세스를 종료. 이는 프로세스를 멈추는 가장 강력한 방법이지만, 데이터 손실이 발생할 수 있다.       
killall <프로세스명>: 특정 프로세스 이름을 가진 모든 프로세스를 종료
``` 

* kill 명령어의 장단점                    
장점: 간단한 명령어로 빠르게 프로세스를 종료할 수 있다.     
      다양한 옵션을 사용하여 프로세스 동작을 제어할 수 있다.       
단점: 잘못 사용하면 의도치 않은 프로세스 종료가 발생할 수 있습니다.               
      SIGKILL 시그널을 사용하여 강제 종료할 경우, 프로세스가 올바르게 정리되지 않을 수 있고, 데이터 손실 등의 문제가 발생할 수 있다.        
