# Cods for graphs
```
digraph call_cc {
    
  "(call/cc proc)" -> "... ● ..." -> ".......";
  "(call/cc proc)" -> "(proc ◻ )" -> "...  ●  ..." -> "........"
  
}


digraph call_cc {
  "( ☐ v)" -> "A: (... ● ...)";
  "( ☐ v)" -> "C: (... ● ...)" -> "D: (... ● ...)" -> ".... ";
  "A: (... ● ...)" -> "B: (... ● ...)" -> "....";
  "-->"
  "C: (... v ...)" -> "D: (... ● ...) " -> " .... ";
}

digraph call_cc {
  "(+ (prod '(2 3 0 5)) 1)" -> "(prod '(2 3 0 5))";
  "(prod '(2 3 0 5))" -> "(+ • 1)";
  "(prod '(2 3 0 5))" -> "(call/cc \n (lambda (c)  \n (prod-rec '(2 3 0 5) c)))" -> "(+ • 1) ";
  "(+ • 1) " -> "(lambda (c) \n (prod-rec xs c) ☐ )" -> "xs | '(2 3 0 5)";
  "(lambda (c) \n (prod-rec xs c) ☐ )" -> " (+ • 1)";
  " (+ • 1)" -> "(prod-rec xs c)";
  "(prod-rec xs c)" -> "xs | '(2 3 0 5) \n c | ☐";
  "xs | '(2 3 0 5) \n c | ☐" -> " (+ • 1) ";
  "(prod-rec xs c)" -> " (+ • 1) ";
  "(prod-rec xs c)" -> "(cond
    ((null? '(2 3 0 5)) 1)
    ((= (car '(2 3 0 5)) 0) (☐ 0))
    (else (* (car '(2 3 0 5))
    (prod-rec (cdr '(2 3 0 5)) ☐)))))" -> " (+ • 1)  ";
  "  --> "
  "(* 2 (prod-rec '(3 0 5) ☐ ))" -> "  (+ • 1) ";
}


digraph call_cc {
    "(call/сc
    (lambla (c)
      (set! b c)
      7)))" -> "(+ 100 ●) " ;
      
  "(+ 100 ●) " -> " REPL"
  "((lambla (c)
      (set! b c)
      7)
      ☐)" -> "(+ 100 ●)"
  "(+ 100 ●)" -> REPL
}


digraph call_cc {
  "(begin
      (set! b ☐)
      7)" -> "(+ 100 ●)" ;
  "(+ 100 ●)" -> REPL ;
  "(+ 100 ●)" -> "(+ 100 7)" ;
  "(+ 100 7)" ->  "REPL " ;
  "(+ 100 7)" -> "напечатается 07";
  "-->"
  "(* 3 (b 22))" -> "REPL  " ;
  "--> "
  "(b 22)" -> "(x 3 ●)" ;
  
  
}


digraph call_cc {
   "(☐ 22)" -> "(+ 100 ●)";
   "b | ☐" -> "(+ 100 ●)" ; 
   "(+ 100 ●)" -> REPL ;
   "(☐ 22)" -> "(* 3 ●)" ;
   "фрейм отбрасывается" -> "(* 3 ●)" ; 
   "(* 3 ●)" -> "REPL ";
   "-->"
   "(+ 100 22)" -> " REPL" -> "напечатается 122";
}
```