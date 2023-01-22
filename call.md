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

![graphviz-13](https://user-images.githubusercontent.com/69920824/213928170-9825b9ee-4ad4-49fb-9968-a2628fe57d42.png)


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

далее переходит в: 

![graphviz-6](https://user-images.githubusercontent.com/69920824/213925958-272f547d-2b02-460f-b871-c5de6a3fbba2.png)


```
(define (REPL)
    (let* (e (read))
          (v (eval e (interaction-enviroment)))
          (- (print v)))
       (REPL)))
(define (print v)
      (write v)
      (newline))
      
(define b #f)
(+ 100 (call/сc
         (lambla (c)
           (set! b c)
           7)))
           
(* 3 (b 22))
```

![graphviz-10](https://user-images.githubusercontent.com/69920824/213927124-d276e51e-93b8-4a19-87c0-890212bf4db8.png)

![graphviz-11](https://user-images.githubusercontent.com/69920824/213927544-f48e9433-8ff8-4740-a0b9-391ca9c4e6fa.png)


![graphviz-12](https://user-images.githubusercontent.com/69920824/213928058-c430f598-839b-4658-b835-54753d95bde3.png)


