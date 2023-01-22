call-with-current-continuation
=================================================
Синтаксис
---------------------------------------------------------
```
(call-with-current-continuation proc)
```
proc - процедура с одним параметром: (proc cont).
 Параметр процедуры proc - это продолжение (continuation, "континуация") cont.
 cont может быть применена как процедура с одним аргументом.
 
Cематика
---------------------------------------------------------
Далее для краткости будет **call/cc** вместо **call-with-current-continuation**.
```
(define call/cc call-with-current-continuation)
```
Процедура **call/cc** создаёт объект продолжения из точки своего применения и к этому объекту применяет свой аргумент.
 Если примененная процедура ничего не делает со своим аргументом, то её возврвщвемое значение становится возвращаемым значением вызова **call/cc**.

![graphviz](https://user-images.githubusercontent.com/69920824/213925045-178a4134-fb7d-49ed-850a-2dcb3576be67.svg)

Применение продолжения
---------------------------------------------------------

Стек, предшествующий применению продолжения, отбрасывается, восстанавливается стек, сохранённый в продолжении. 

![graphviz-2](https://user-images.githubusercontent.com/69920824/213925216-b32c47a6-886d-449c-b469-91c5572d5091.png)

Переходит в:

![graphviz-3](https://user-images.githubusercontent.com/69920824/213925250-d865c9b1-0431-4f9c-9edb-9ec52140ef7b.png)

 ```
(define (prod-rec xs c)
  (cond
    ((null? xs) 1)
    ((= (car xs) 0) (c 0))
    (else (* (car xs)
             (prod-rec (cdr xs) c)))))
             
(define (prod xs)
  (call/сc
   (lambla (c)
           (prod-reс xs c))))
```

![graphviz-7](https://user-images.githubusercontent.com/69920824/213925781-da22c85d-8fe6-4c96-b889-0ba523a16140.png)

переходит в:

![graphviz-6](https://user-images.githubusercontent.com/69920824/213925958-272f547d-2b02-460f-b871-c5de6a3fbba2.png)








#  ⇩  ➪

