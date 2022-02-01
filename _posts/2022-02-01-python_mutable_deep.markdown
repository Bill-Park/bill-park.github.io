---
layout: post
title:  "Python에서 mutable 형의 특징"
categories: [coding]
---

python은 type을 엄격하게 검사하거나, 요구하지 않습니다. type 함수를 통해 변수의 type을 확인할 수는 있으나 변수의 type이 고정되어있지 않아 int 값을 추가했다가 str값을 추가하는 등 다용도로 사용이 가능합니다.

변수와 관련된 업데이트로는 Python 3.5에서 PEP 484(Type Hint), 3.6버전에서 PEP 526(Variable Annotations), 3.10에서 PEP 604(Type Union Operator)가 추가되었습니다. 이렇게 최근에 Python에서는 변수와 관련된 업데이트를 진행한 것을 볼 수 있는데, 과거에 비해 변수의 type에 대해 엄격해진다고 생각하고 있습니다.

Python에서 변수는 객체이고, 어떤 특징을 가지는지는 다른 분들이 잘 써주셨으니 mutable과 immutable로 바로 넘어가겠습니다. 쉽게 설명하면 mutable은 만들어진 후 값을 변경할 수 있으며 immutable은 값을 변경할 수 없습니다. 

immutable 형에 속하는 대표적인 type은 아래와 같습니다.

- number
- string
- tuple

mutable에 속하는 대표적인 type은 아래와 같습니다.

- dictionary
- list

id 함수를 이용하면 변수의 ID(identity)값을 확인할 수 있습니다. CPython 내부에서 객체의 주소값을 의미합니다.

변수의 값을 변경한 후 id 함수를 이용하면 immutable인지 mutable인지 알 수 있는데 예시를 살펴보겠습니다.

```python
a = 1
print(id(a)) # 140721345503632
a = '1'
print(id(a)) # 2838386330352
```

immutable 값인 1, ‘1’을 넣었을 때 변수 a의 id값 또한 변경된 것을 볼 수 있습니다.

```python
c = [1, '1']
print(c) # [1, '1']
print(id(c)) # 2838469757640
c.append(2)
print(c) # [1, '1', 2]
print(id(c)) # 2838469757640
```

반면 mutable인 list 형의 경우 변수 값이 바뀌었어도 자체의 id값은 바뀌지 않았습니다.

mutable 변수를 다른 변수에 대입하는 경우 2가지 경우의 수가 있습니다. list형을 예로 들어 설명하겠습니다.

```python
d = [1, 2, 3]
e = d # 동일한 객체 복사
f = d[:] # 슬라이싱을 통해 새 list를 생성하여 대입
print(id(d)) # 2838469719624
print(id(e)) # 2838469719624
print(id(f)) # 2838469757128
```

list형 변수 d를 생성하여 e에 그대로 대입한 경우 id가 동일하게 출력됩니다. 변수 대입시 reference(참조값)를 복사하여 대입하기 때문에 id가 동일한 것입니다. 반면 f의 경우 d를 슬라이싱하여 새로운 list(새 instance)를 생성하여 대입하기 때문에 id값이 다른 것입니다.

조금 복잡하게 list 안의 list를 만들어서 id를 확인해보겠습니다.

```python
l = [1, 2, 3]
l_1 = [4]
print(l, id(l)) # [1, 2, 3] 2838469751496
print(l_1, id(l_1)) # [4] 2838469757448
l.append(l_1) # l에 l_1을 추가, l_1의 reference가 추가됨
print(l, id(l)) # [1, 2, 3, [4]] 2838469751496
print(l_1, id(l_1)) # [4] 2838469757448
l_1.append(5)
print(l, id(l)) # [1, 2, 3, [4, 5]] 2838469751496
```

l에 l_1을 추가하여도 l의 id가 바뀌지 않는 것은 위에서 확인하였습니다. 그러면 l_1을 바꾸면 어떻게 될까요? l에 추가된 l_1은 l_1의 reference이므로 l_1의 값이 변경되면 l의 값 또한 바뀌게 됩니다. 하지만 id는 여전히 동일합니다.

여기에서 같은 mutable 형인 dict로 넘어가 보겠습니다. 새 dict를 생성하는 방법은 여러가지가 있는데 대표적으로 중괄호를 이용한 방법, dict 생성자를 이용한 방법이 있습니다. key가 a, b, c이면서 value는 전부 빈 dict로 되어있는  dict 2개를 생성해 보겠습니다.

```python
d_1 = {'a': {}, 'b': {}, 'c': {}}
d_names = ['a', 'b', 'c']
d_2 = dict.fromkeys(d_names, {})
print(d_1, id(d_1)) # {'a': {}, 'b': {}, 'c': {}} 2838469768120
print(d_2, id(d_2)) # {'a': {}, 'b': {}, 'c': {}} 2838469862168
```

값은 동일하지만 id는 다른것을 볼 수 있습니다. 여기에 각 value의 id를 확인해보겠습니다.

```python
print(id(d_1['a']), id(d_1['b']), id(d_1['c'])) # 2838469750040 2838469769000 2838469750120
print(id(d_2['a']), id(d_2['b']), id(d_2['c'])) # 2838469749640 2838469749640 2838469749640
```

중괄호로 생성한 d_1은 각 value의 id가 다르지만, fromkeys를 이용한 경우 동일한 id를 가지고 있습니다. 해당 내용은 python 공식 문서([링크](https://docs.python.org/3/library/stdtypes.html#dict.fromkeys))에도 나와있습니다.

> [fromkeys()](https://docs.python.org/3/library/stdtypes.html#dict.fromkeys) is a class method that returns a new dictionary. *value* defaults to `None`. All of the values refer to just a single instance, so it generally doesn’t make sense for *value* to be a mutable object such as an empty list. To get distinct values, use a [dict comprehension](https://docs.python.org/3/reference/expressions.html#dict) instead.
> 

mutable object에 속하는 빈 dict를 value로 이용하였으므로 d_1[’a’], d_1[’b’], d_1[’c’] 전부 같은 instance를 가리키고 있습니다. 이 때 하위 dict를 변경하면 어떻게 되는지 살펴보겠습니다.

```python
d_1['a']['aa'] = [1, 2, 3] # d_1은 각 value의 id가 다르므로(별개의 레퍼런스를 가짐) 변하지 않음
print(d_1) # {'a': {'aa': [1, 2, 3]}, 'b': {}, 'c': {}}
d_2['a']['aa'] = [1, 2, 3] # d_2는 각 value의 id가 같음
print(d_2) # {'a': {'aa': [1, 2, 3]}, 'b': {'aa': [1, 2, 3]}, 'c': {'aa': [1, 2, 3]}}

d_2['a'] = {'bb' : [4, 5, 6]} # 이 경우는 d_2['a']에 새로운 dict의 레퍼런스가 들어감 -> d_2['b']에 영향을 주지 않음
print(d_2) # {'a': {'bb': [4, 5, 6]}, 'b': {'aa': [1, 2, 3]}, 'c': {'aa': [1, 2, 3]}}
```

d_2에 속한 각 pair의 instance가 동일하므로 하나의 instance 값이 바뀌면 다른 모든 pair의 value가 바뀌는 것을 볼 수 있습니다. 각 value의 reference는 유지된 채 값이 바뀌었기 때문입니다.

반면 새로운 instance를 생성하여 대입하는 경우 value의 reference 자체가 바뀌므로 다른 pair에는 영향을 주지 않습니다.

이는 unpacking을 이용한 경우에도 주의해야 합니다.

```python
d_3 = {**d_2} # dictionary unpacking을 통한 대입, list slicings과 유사함
print(id(d_2)) # 2838469862168
print(id(d_2['b']), id(d_2['c'])) # 2838469749640 2838469749640
print(id(d_3)) # 2838469731496
print(id(d_3['b']), id(d_3['c'])) # 2838469749640 2838469749640
```

list의 슬라이싱과 유사한 unpacking을 이용하여 d_2를 unpacking하여 d_3에 대입하였습니다. d_2와 d_3의 id값을 보면 둘은 전혀 다른 instance임을 볼 수 있지만, 하위 pair의 value의 id는 동일하기 때문에 주의가 필요합니다.

Python에서 mutable을 어떻게 다루고 있는지 조금 자세하게 알아보았습니다. reference(instance의 주소값), instance(생성 완료된 변수 object), id등 처음보는 용어나 개념도 있었을 것이라 생각됩니다. 잘못된 내용이나 수정해야할 부분이 있다면 언제든지 알려주시면 반영하도록 하겠습니다.