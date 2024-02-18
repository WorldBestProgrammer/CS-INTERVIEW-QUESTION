# 프로세스 메모리 구조에서 BSS segment와 Data segment를 나눈 이유는 무엇인가

---

프로세스 메모리 구조는 아래와 같다.

BSS는 아직 초기화되지 않은 static 변수를 가지고 있다.
반면 Data는 초기화된 변수를 가지고 있다.
![Process Memory Structure](https://gabrieletolomei.files.wordpress.com/2013/10/program_in_memory2.png)
이렇듯 초기화 여부를 기준으로 영역을 나눈 이유는 
프로그램이 메모리에 로드될 때 초기화된 변수는 실행파일에 명시되어 있는 값들을 가지고 오게 된다. 
그러나 초기화되지 않은 변수는 0으로만 초기화하면 되기 때문에 명령어를 한 줄만 읽으면 된다.
즉, 이 둘은 초기화하는 과정이 다른 것이다. 아래와 같이 생각하면 된다.
``` c
for(i=0; i<all_explicitly_initialized_objects; i++)
{
.data[i] = init_value[i];
}

memset(.bss,
0,
all_implicitly_initialized_objects);
```
따라서 이 둘의 영역을 분리한 것이다. 
이렇게 되면 각 영역 별로 해당하는 초기화 과정을 진행해주면 되기 때문에 성능상의 이점이 있다. 

# 꼬리 질문

--- 

## BSS에는 초기화되지 않은 변수가 저장된다. 왜 초기화되지 않은 변수를 만든 것일까?

---
아래의 코드를 보면 a는 초기화되지 않은 배열 변수이고 b는 초기화된 배열 변수이다.
``` c++
int a[4];
int b[] = { 1 , 2 , 3 , 4 };

int main()
{}
``` 
위 코드가 컴파일이 되어 어셈블리어가 되면 다음과 같이 된다.
``` assembly
a:
    .zero   16
b:
    .long   1
    .long   2
    .long   3
    .long   4
main:
    pushq   %rbp
    movq    %rsp, %rbp
    movl    $0, %eax
    popq    %rbp
    ret
```
위에서 볼 수 있듯이 a는 한 줄이면 되지만 b는 배열의 각 원소마다 초기화되어야 하는 값이 명시가 되어 있어야 한다.
즉, 이렇게 하면 값이 당장 초기화해야 하지 않을 상황에서는 프로그램의 사이즈를 줄일 수 있게 된다. 또한 메모리에 공간을 할당하고 0으로 초기화만 하면 되기 때문에 메모리에 로드하는 시간도 줄어들게 된다.
### Reference

---
- https://gabrieletolomei.wordpress.com/miscellanea/operating-systems/in-memory-layout/  
- https://stackoverflow.com/questions/9535250/why-is-the-bss-segment-required  
- https://stackoverflow.com/questions/21350478/what-does-memory-allocated-at-compile-time-really-mean
