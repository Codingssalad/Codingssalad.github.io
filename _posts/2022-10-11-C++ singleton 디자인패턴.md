# C++ singleton 디자인 패턴`

Singleton은 전역변수 개선된 것 입니다.

싱글턴을 사용할 때는 application에서 하나의 객체만 사용합니다.
이번 글에서는 C++에서 singleton 패턴을 구현하는 방법에 대해서 공부해보려고 합니다.

지난 글에서 배웠던 생성자와 소멸자에 대한 지식을 알고있으며,
접근 지시자에 대한 내용을 알고 있으시면 이해하기에 어려움이 없을거라고 생각합니다.

먼저 class의 내용을 먼저 확인해보겠습니다.

여기서 잘봐야 하는것은 생성자가 private 접근지시자 안에 선언되어 있는 것 입니다.

private은 객체 자신만이 접근할 수 있도록 하는 것 인데요,

생성자를 private에 두면 ? 자기 자신의 클래스 안에서만 객체를 생성할 수 있습니다.

그러면 외부에서는 객체를 선언할 수 없어요.
그래서 public 부분에 get_instance라는 함수를 통해서 객체를 만들 수 있도록 합니다.

이때 이 instance라는 변수를 static으로 선언하여 언제 호출하여도 단 하나의 객체만 호출되도록 합니다.

static 변수는 전연변수 처럼 코드블럭을 벗어나도 없어지지 않는 변수 입니다.

```cpp
class SingletonClass 
{
  private:
    //constructor is located in private
    SingletonClass()
    {
      std::cout << "This is constructor this method is called when class is created" << std::endl;
    }
    //destructor
    ~SingletonClass()

  public:
    static SingletonClass& get_instance()
    {
        static SingletonClass instance;
        return instance;
    }
    int m_data;
};
```

아래 코드를 실행해보겠습니다.

```cpp
#include <iostream>
#include <memory>

class SingletonClass 
{
  private:
    //constructor
    SingletonClass()
    {
      std::cout << "This is constructor this method is called when class is created" << std::endl;
    }
    //destructor
    ~SingletonClass()
    {
      std::cout << "This is destructor this method is called when class is deleted" << std::endl;
    }

  public:
    static SingletonClass& get_instance()
    {
        static SingletonClass instance;
        return instance;
    }
    int m_data;
};

int main(){
  SingletonClass &T1 = SingletonClass::get_instance();
  T1.m_data = 10;
  std::cout << "T1.m_data = " << T1.m_data << std::endl;
  SingletonClass &T2 = SingletonClass::get_instance();
  std::cout << "T2.m_data = " << T2.m_data << std::endl;
  
  SingletonClass &T3 = SingletonClass::get_instance();
  T3.m_data = 20;

  std::cout << "T1.m_data = " << T1.m_data << std::endl;
  std::cout << "T2.m_data = " << T2.m_data << std::endl;
  std::cout << "T3.m_data = " << T3.m_data << std::endl;
}
```

그러면 T1,T2,T3 객체를 생성해도 get_instance 함수에서  return해주는 동일한 객체를 가져오게 되는 것 입니다.

실행결과를 확인하면 T3를 변경해도 T1,T2의 값이 전부 변경되는 것을 확인할 수 있습니다.