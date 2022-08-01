---
title: "Function and Arguments"
categories:
- Python
- Assignment
output:
 html_document:
   keep_md: true
date: '2022-06-28 18:00:00'
---
# Unit 30


```python
print(10,20,30)
```

    10 20 30
    


```python
def print_numbers(a,b,c):
  print(a)
  print(b)
  print(c)
print_numbers(10,20,30)
```

    10
    20
    30
    

## 언패킹 사용


```python
x=[10,20,30]
print_numbers(*x)
print_numbers(*[10,20,30])
```

    10
    20
    30
    10
    20
    30
    

## 가변 인수 함수 만들기
```
def 함수이름(*매개변수):
  코드
```


```python
def print_numbers(*args):
  for arg in args:
    print(arg)
print_numbers(10)
print_numbers(10,20,30)
```

    10
    10
    20
    30
    


```python
x=[10]
print_numbers(*x)
y=[10,20,30,40]
print_numbers(*y)
```

    10
    10
    20
    30
    40
    

## 키워드 인수 사용


```python
def personal_info(name,age,address):
  print('이름 : ',name)
  print('나이 : ',age)
  print('주소 : ',address)
personal_info('홍길동',30,'경기')
```

    이름 :  홍길동
    나이 :  30
    주소 :  경기
    

### 키워드 인수 방식


```python
personal_info(name='홍길동',age=30,address='경기') # 순서를 맞추지 않아도 입력가능
```

    이름 :  홍길동
    나이 :  30
    주소 :  경기
    

### 딕셔너리 언패킹 



```python
def personal_info(name,age,address):
  print('이름 : ',name)
  print('나이 : ',age)
  print('주소 : ',address)
```


```python
x={'name': '홍길동', 'age':30, 'address':'경기'}
personal_info(**x) # *을 한번 사용하면 키가 출력, 두번사용하면 value를 출력
```

    이름 :  홍길동
    나이 :  30
    주소 :  경기
    

### 키워드 인수를 사용하는 가변 인수 함수 만들기 
```
def 함수이름(**매개변수):
  코드
```


```python
def personal_info(**kwargs):
  for kw, arg in kwargs.items():
    print(kw, ': ', arg, sep='')
```


```python
personal_info(name='홍길동')
print('-------------')
personal_info(name='홍길동', age=30,address='경기')
```

    name: 홍길동
    -------------
    name: 홍길동
    age: 30
    address: 경기
    


```python
x={'name':'홍길동'}
personal_info(**x)
```

    name: 홍길동
    

- 보통 특정 키가 있는지 확인한뒤 기능을 만든다


```python
def personal_info(**kwargs):
    if 'name' in kwargs:    # in으로 딕셔너리 안에 특정 키가 있는지 확인
        print('이름: ', kwargs['name'])
    if 'age' in kwargs:
        print('나이: ', kwargs['age'])
    if 'address' in kwargs:
        print('주소: ', kwargs['address']) 
```

## 매개변수 초깃값 지정
```
def 함수이름(매개변수=값):
  코드
``` 
- 인수를 생략할 때 초깃값 지정
- 초깃값이 지정된 매개변수는 맨뒤쪽으로 빼야한다


```python
def personal_info(name, age, address='비공개'):
  print('이름: ', name)
  print('나이: ', age)
  print('주소: ', address)

```


```python
personal_info('홍길동',30) # 인수를 생략하면 초깃값으로 출력
```

    이름:  홍길동
    나이:  30
    주소:  비공개
    

## Practice 


```python
korean, english, mathematics, science = 100, 86, 81, 91
def get_max_score(*args):
  return(args)

max_score = get_max_score(korean, english, mathematics, science)
print('높은 점수:', max_score)
 
max_score = get_max_score(english, science)
print('높은 점수:', max_score)
```

    높은 점수: (100, 86, 81, 91)
    높은 점수: (86, 91)
    

# Unit 29 

## Practice 

### 몫과 나머지를 구하는 함수 만들기 


```python
x=10
y=3

def get_quotient_remainder(a,b): 
  """
  a = int
  b = int
  함수를 실행 시 x를 y로 나눈 몫, 나머지를 출력
  """
  return a//b, a%b 
quotient,remainder = get_quotient_remainder(x,y)
print('몫:{0}, 나머지:{1}'.format(quotient,remainder))
```


      File "<ipython-input-43-0819549c81f4>", line 8
        return a//b, a%b
        ^
    IndentationError: unexpected indent
    

