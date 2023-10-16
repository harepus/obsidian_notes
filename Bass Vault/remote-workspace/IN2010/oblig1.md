```scss
push_back(x):
1. Insert x into backDeque. 
2. If size(backDeque) > size(frontDeque) + 1:
	2.1. Move the front element of backDeque to the back of frontDeque.
```
___
```scss
push_front(x):
    1. Insert x into frontDeque.
    2. If size(frontDeque) > size(backDeque):
        2.1. Move the back element of frontDeque to the front of backDeque.
```
___
```scss
push_middle(x):
    1. If size(frontDeque) == size(backDeque):
        1.1. Insert x into frontDeque.
    2. Else if size(frontDeque) > size(backDeque):
        2.1. Move the back element of frontDeque to the front of backDeque.
        2.2. Insert x into frontDeque.
    3. Else:
        3.1. Insert x into backDeque.
```
___
```scss
get(i):
    1. If i < size(frontDeque):
        1.1. Return frontDeque[i]
    2. Else:
        2.1. Return backDeque[i - size(frontDeque)]
```
___

