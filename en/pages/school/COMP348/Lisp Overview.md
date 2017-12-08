# Common Lisp 

## Basic syntax

- Always (**function-name** arguments)
- Infix everything
    * `(* 2 3 4) = 24`
    * `(< 1 3 2) = NIL` (1 < 3 < 2).

- To prevent subexpressions being evaluated, quote them:
    * `(/ (* 2 6) 3) = 4`
    * `'(/ (* 2 6) 3) = (/ (* 2 6) 3)`

- When calling an arithmetic operator as a fn argument, use `#'*` , `#'+`

## Lists

### List Creation

#### `Cons`

- Creates a list by adding an element as the head of an existing list
- All lists are singly-linked.
    - Each node has two pointers:
        - 1) to the data element
        - 2) To the tail of the list
    - The last node's 2nd pointer points to `()`.

```
> (cons 'a '())
(A)

> (cons 'a (cons 'b '()) )
(A B)

```

#### `list`

- Creates a list comprised of its arguments. Takes any number of arguments and returns a list.

```
> (list 1 2 ’a 3)
(1 2 A 3)

> (list 1 ’(2 3) 4)
(1 (2 3) 4)

> (list ’(+ 2 1) (+ 2 1))
((+2 1) 3)

> (list 1 2 3 (list ’a ’b 4) 5) 
(1 2 3 (A B 4) 5)
```

#### `append`

- Append takes ONLY LISTS. Syntax error for non-lists.  
- Creates a list by concatenating existing lists  

```
> (append '(1 2) '(3 4))
(1 2 3 4)

> (append '(1 2 3) '() '(a) '(5 6))
(1 2 3 A 5 6 )
```

### List Access

- `car`, or `first` - returns head
    * `(car '(a s d f)) -> A`
- `cdr`, or `rest` - returns tail as a list
    * `(cdr '(a s d f)) -> (s d f)`

## Truth Values

- True/False -> `t`/`nil`
- `(not t)` -> `nil`, `(not nil)` -> `t`
- Functions with boolean return values called 'predicates' in Lisp

- `listp`  returns true if argument is a list:
    * `(listp '(a b c) )` -> `T`

- `numberp arg` -> true if `arg` is a number
- `zerop arg` -> true if `arg` is zero
- `evenp arg` -> true if `arg` is even
- `oddp arg` -> true if `arg` is odd

### `if`

```lisp
( if *testExpr* *thenExpr* )  
( if *testExpr* *thenExpr* *elseExpr* )  
```
So if (*predicate* *expression* *expression*).

### `cond`

```lisp
( cond (q1 a1) (q2 a2) ... (else an) )
```

For the first `q` to eval true, then the corresponding `a` is evaluated and returned
If no `q` evals true, returns the `an` value

## Variables

### Binding

- `let` assigns variables to a limited scope
    * `(let ((x 2) (y 3) ) (+ x y)` -> 5

- `let*` allows value of new variable to depend on value established by same expr.

- Global : `setq *name* *value*`
- Local : `setf *name* *value*`

- `eql` -> true if arguments point to **same object**
- `equal` -> true if arguments point to **same value**

## Data Type

### List

`(a) == (cons 'a '()) == (cons 'a nil)`
n.b. `(cons 'a)` is a syntax error, not enough args

## Functions

### `defun`

( defun *name* (*formal parameter list*) body )  

ex. 

```
(defun absdiff (x y)
    (if (> x y)
      (- x y)
      (- y x)))
```

### Higher order functions

- `mapcar`: takes as its arguments a function and one (or more) lists and applies the function to the elements of the list(s) in order.
- `funcall`: takes as its arguments a function and a list of arguments (does not require arguments to be packaged as a list), and returns the result of applying the function to the elements of the list.
- `apply` works like `funcall`, but requires that the last argument is a list.

### Anonymous / Lambda functions

`(lambda (*formal parameter list*) (*body*) )`

ex. `( (lambda (x) (* x x )) 3 ) ` -> 9 

### Recursive definitions

1) Base case: If lst1 is empty, then return lst2.
2) Recursive case: Return a list containing as its first element the head of lst1 with its tail being the concatenation of the tail of lst1 with lst2.

```
(defun append2 (lst1 lst2)
    (if (null lst1)
      lst2
      (cons (car lst1) (append2 (cdr lst1) lst2))))
```



1) Base case: If the list is empty, then sum is 0.
2) Recursive case: Add the head element to the sum of the elements of the tail.  

```
(defun sum (lst)
  (cond ((null lst) 0)
        (t (+ (car lst) (sum (cdr lst))))))
```
```
(sum '(1 2 3)):
(+ 1 sum '(2 3))
(+1 (+ 2 (sum '(3))
(+1 (+ 2 (+ 3 )))
= 6
```


##MISC

### PRINT

```lisp
(print '(a b c)) - 

(A B C)
(A B C)

[2]> (print '('a 'b 'c))

('A 'B 'C)
('A 'B 'C)

[3]> (print '('(a b) '(c) ))

('(A B) '(C))
('(A B) '(C))

[4]> (print '( (a b) c ))

((A B) C)
((A B) C)

[5]> (print '( () '() '() ))

(NIL 'NIL 'NIL)
(NIL 'NIL 'NIL)

[6]> (print '( () () () ))

(NIL NIL NIL)
(NIL NIL NIL)

[7]> (print '( 1 2 3 ))

(1 2 3)
(1 2 3)
[8]> (print ( 1 2 3 ))

*** - EVAL: 1 is not a function name; try using a symbol instead

### CONS

[10]> (print (cons 1 ()))

(1)
(1)

[11]> (print (cons '1 ()))

(1)
(1)

[12]> (print (cons 'a (cons 'b (cons 'c ()))))

(A B C)
(A B C)

###LIST

[13]> (print (list 'a 'b 'c ))

(A B C)
(A B C)

14]> (print (list a b c ))

*** - SYSTEM::READ-EVAL-PRINT: variable A has no value

[16]> (print (list '(a) '(b) '(c) ))

((A) (B) (C))
((A) (B) (C))
```
