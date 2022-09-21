# Selenium 실습하기
## Keys 종류를 알아보기


```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys # 실습을 위해 Keys 라이브러리를 import 합니다.
from selenium.webdriver.common.by import By
```

#### 이번에도 네이버 홈 화면을 사용하여 실습해보겠습니다.
#### 먼저 아래 코드를 실행하여 Chrome driver를 사용하여 naver.com 으로 이동합니다.


```python
driver = webdriver.Chrome()
url = "https://www.naver.com"

driver.get(url)
```

#### F12키를 눌러 Keys를 활용하여 검색창 부분을 클릭하고, 입력을 해보겠습니다.
#### xpath ID = //*[@id="query"] 입니다.
#### 먼저 xpath로 찾은 값을 Search 라는 변수에 저장합니다.


```python
Search = driver.find_element(By.XPATH,'//*[@id="query"]')
```


```python
Search.click() # 클릭하기
```

#### 다음으로 Keys를 활용하여 값을 입력해보겠습니다.


```python
Search.send_keys("Python Crawling")
```

#### 검색어를 입력했으니, 엔터를 눌러 보겠습니다.
#### Keys.RETURN을 입력하면 엔터키가 눌려지게 되요


```python
Search.send_keys(Keys.RETURN)
```

#### Ctrl + V 와 같은 키 조합을 입력하는 것도 가능 합니다.
#### 복사 붙여넣기 기능을 사용할 때는 pyperclip을 사용하면 유용합니다.
#### python에서 클립보드를 사용할 수 있도록 해주는 라이브러리 입니다.
#### 아래와 같이 하면 됩니다.


```python
import pyperclip # import 
```


```python
pyperclip.copy("Hello")
driver.find_element_by_xpath('//*[@id="nx_query"]').send_keys(Keys.CONTROL + 'v') # 붙여넣기
```

    C:\Users\QCELLS\AppData\Local\Temp\ipykernel_28168\705333455.py:2: DeprecationWarning: find_element_by_xpath is deprecated. Please use find_element(by=By.XPATH, value=xpath) instead
      driver.find_element_by_xpath('//*[@id="nx_query"]').send_keys(Keys.CONTROL + 'v') # 붙여넣기
    

#### 당연히 CTRL + A 등과 같은 동작도 가능합니다.
#### 지금 입력되어 있는 값을 모두 선택해보겠습니다!


```python
driver.find_element_by_xpath('//*[@id="nx_query"]').send_keys(Keys.CONTROL + 'a') # 붙여넣기
```

    C:\Users\QCELLS\AppData\Local\Temp\ipykernel_28168\3852222455.py:1: DeprecationWarning: find_element_by_xpath is deprecated. Please use find_element(by=By.XPATH, value=xpath) instead
      driver.find_element_by_xpath('//*[@id="nx_query"]').send_keys(Keys.CONTROL + 'a') # 붙여넣기
    

#### Keys.DELETE를 입력하면 지우기 동작이 됩니다.
#### 지금 상태에서는 검색창에 "Python CrawlingHello" 라는 글이 입력되어 있고,
#### CTRL+A를 눌러 모두 선택했습니다.
#### Keys.DELETE를 하여 선택된 부분이 삭제되는지 보겠습니다.


```python
driver.find_element_by_xpath('//*[@id="nx_query"]').send_keys(Keys.DELETE) # 붙여넣기
```
