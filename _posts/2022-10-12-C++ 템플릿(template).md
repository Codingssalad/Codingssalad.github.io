# 작성중 - C++ 템플릿

안녕하세요,

이번에는 Template에 대해서 알아보도록 하겠습니다.

객체 지향 프로그래밍의 중요한 개념 중 하나는 바로 overloading 이라고 했었는데요,

같은 이름의 함수를 여러 개 만들 수 있으며, 호출 되는 매개변수에 따라서 적합한 함수가 호출되는 방식 입니다.

예를 들어서 아래와 같이 오버로딩을 할 수 있습니다.

print라는 함수에 매개변수가 int 인지 const char* 인지에 따라서 호출되는 함수가 다른 것 이지요.

```cpp
void print(int a)
{
	std::cout << "int : " << a << std::endl;
}

void print(const char* a)
{
	std::cout << "str : " << a << std::endl;
}

void print(float a)
{
	std::cout << "float :" << a << std::endl;
}

void print(double a)
{
	std::cout << "double :" << a << std::endl;
}
```

하지만 C++ 개발자들은 매개변수의 타입에 대해서도 범용성 있게 코드를 짜기 위한 아이디어를 냈습니다. 그게 바로 C++의 template 입니다.

위 코드를 Template을 활용하여 작성하면 이렇게 작성할 수 있습니다.

```cpp
#include <iostream>

template <typename _Template>
void print(_Template T){
  std::cout << "typeid = " << typeid(T).name() << "\tval = " << T << std::endl;
}
```

아래와 같이 main안에서 print 함수를 호출하여 얻어지는 결과를 보면,

전달되는 매개변수가 달라도 모두 동작이 되는 것을 확인할 수 있습니다.

```cpp

int main(){
  print("Hello");  // string 출력
  print(3.14);     // double 출력
  print(5.16f);    // float 출력
  print(100);      // int 출력
}
---------------------------
실행 결과 :
---------------------------
typeid = PKc    val = Hello
typeid = d      val = 3.14
typeid = f      val = 5.16
typeid = i      val = 100
---------------------------
```

간단한 예제를 통해서도 보이듯 template을 이용하여 사용하면 코드의 양이 줄어들고,

쉽게 사용을 할 수 있어집니다.

Template을 사용하는 것 중 가장 많이 사용되는 것은 바로 vector 입니다.

vector클래스는 보면 template으로 구현이 되어있다는게 보이죠! 역시 아는 만큼 보이는 것 같습니다.

```cpp
template<typename _Tp, typename _Alloc = std::allocator<_Tp> >
    class vector : protected _Vector_base<_Tp, _Alloc>
    {
...
...
...
		}
```

벡터가 템플릿으로 구현이 되어있기 때문에, 꺽쇠< > 안에 어떤 값을 넣어도 만들기가 가능한 것 입니다. 만약 템플릿으로 구현되지 않았다면, 모든 자료형에 대해서 오버로딩 함수가 구현되어야 했겠죠?

템플릿으로 구현되어 있기 때문에 vector<자료형(template)> 변수이름;을 
통해서 각각의 타입을 갖는 vector를 만들어내는 것이 가능해지는 것 입니다.

```cpp
#include <vector>
#include <iostream>

int main()
{
    using namespace std;
    vector<int> v1;
    vector<float> f1;
    vector<std::string> s1;

    v1.push_back(1);
    f1.push_back(3.14f);
    s1.push_back("Hello");

    std::cout << v1.at(0) << std::endl;
    std::cout << f1.at(0) << std::endl;
    std::cout << s1.at(0) << std::endl;
}
```

이상으로 C++ 템플릿의 개념을 간단하게 확인해 보았습니다.