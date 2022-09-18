# 레퍼런스 사용하기
## 레퍼런스를 사용할 때는, 변수 선언할 때 자료형 뒤에 "&"를 추가하면 됩니다.
## 아래의 코드에서 int& a_Refernce는 a 라는 변수 참조에 사용되는 변수 입니다.
## 출력을 해보면 두개 모두 같은 "10" 즉, a에 저장된 값을 출력하는 것을 확인할 수 있습니다.

```c++
#include <iostream>

```

```c++
int a = 10;
```


```c++
int& a_Reference = a;
```


```c++
std::cout << a << std::endl;
```

    10



```c++
std::cout << a_Reference << std::endl;
```

    10


# 레퍼런스 값 변경하기
## a_Reference는 변수 a를 참조하고 있습니다.
## 두개 중 한개의 값을 변경한다면, 다른 변수도 값이 변경 됩니다.
### refernce 값을 변경한 결과를 확인해보세요!


```c++
a_Reference = 918;
```


```c++
std::cout << a << std::endl;
```

    918



```c++
std::cout << a_Reference << std::endl;
```

    918


# 레퍼런스 전달 함수와 일반 함수 차이
## 함수를 호출할 때 값 전달에도 레퍼런스를 사용할 수 있습니다
## Sum_ref는 레퍼런스 값이 전달 됨
## 레퍼런스로 전달된 경우 원본 값이 변경 됩니다.


```c++
void Sum_ref(int& A){
    A = A + 100;
}
```


```c++
a = 100;
```


```c++
Sum_ref(a)
```


```c++
a
```




    200



## Sum_normal은 매개변수가 값으로 전달 됨
## 원본 값인 a는 변하지 않는것을 확인할 수 있습니다.


```c++
void Sum_normal(int A){
    A = A + 100;
}
```


```c++
a = 100;
```


```c++
Sum_normal(a);
```


```c++
a
```




    100




```c++

```
