#Prolog 

## Concepts

### Arithmetic

- tl;dr, use `is` keyword if you want arithmetic evaluated

### Unification

- if a query matches a rule, it **unifies** with it. Goes in sequence.
    * If it's a ground query, unifies with a statement.
    * If it's non-ground, Prolog seeks **instantiations** that could make the query succeed.
- The process of taking two atoms (one from head, one from rule) and determining if there exists a substitution that makes them the same.

### Instantiation

e.g. `parent(X,tom)`

- Prolog scans from top to bottom to find **instantiations** of `X` that make `parent(X,tom)` true.
- Same thing for multiple variables as in `parent(X,Y)`. Prolog tries first `X` and pairs with each `Y` that could make it true, continues to the next `X`, etc.

### Resolution

- When an instantiation is found, Prolog **resolves** to a new query.
- When an atom from the query has been unified with the head of a rule, resolution replaces the atom with the **body** of the rule and applies the substitution to the new query. 

## Variables

- Variables always start with `_` or a capital letter
- Variables are immutable
- Anonymous variable `_` matches anything
    * will match a list, the head, the tail, but not an unspecified sequence

## Builtin functions

`findall(X,P,L)`: returns a list L with all values for X that satisfy predicate P. 
`list_to_set(List,Set)`: returns a set from a list (removes redundancies)


## Lists

- `[H|T]` unifies with any list, except the empty one, even those of length 1.
    * `H` will be the element, `T` will be `[]`

### Iterating through a list

```
contains(Item,[Item|Rest]).
contains(Item,[_|Rest]) :- contains(Item,Rest).
```

### Constructing a list

    append([], List, List). // empty list + list = list
    append([Head|Tail], List2,[Head|Result]):- append(Tail, List2, Result).

#### Explanation:
- We iterate using the discarded head, but we need to keep it to add to the result.
- This says search through the first list, and stick the first thing on the first list to the resulting one.

```
append([b,c],[d,e],Result)
append([c],[d,e], Result)
append([],[d,e], Result) // which matches a rule and exits recursion
```


NOW:

    append([a|[b,c]], List2, [a|Result]) :- append([], List2, Result) // result gets [a|Result]
    append([b|[c]], List2, [b|Result]) :- append([c], List2, Result) // result gets [b|Result]
    append([c|[]], List2, [c|Result]) :- append([b,c], List2, Result) // result gets [c|Result]

FINALLY: 

    Result is [a,b,c,d,e].

### Accessing/querying list

#### First element in list

`first(F,[F|_]).`

#### Last element in list

`last(L,[L]).`
`last(X,[_|T]) :- last(X,T).`

#### Length of list

`length(0,[]).`
`length(Len,[_|T]) :- Len is Sublen + 1, length(Sublen,T).`

#### Prefix/Suffix of list

`prefix(P,L) :- append(P,_,L).`  
`suffix(S,L) :- append(_,S,L).`  
Reads as: if the concatenation of P and any list is L, then P is the prefix of L.

#### Sublist

`sublist(S,L) :- append(_,S,X), append(X,_,L).`

#### Second to last element

```
secondLast([X,_], X).
secondLast([_|T], X) :- secondLast(T, X).
```

#### List is sorted (ascending)

```
ordered([]) .
ordered([_]) .
ordered( [X,Y|Z] ) :- X =< Y , ordered( [Y|Z] ) .
```

#### List is sorted (descending)

```
revOrdered([]) .
revOrdered([_]) .
revOrdered( [X,Y|Z] ) :- X >= Y , revOrdered( [Y|Z] ).
```

#### Return true if only one element.

(Without using/defining size or length functions)

`onlyOne( [ _|[] ] ).`





### Insert in list
 
#### Insert at head of list

`insert_element(R,L, [R|L]).`

#### Insert at nth point

```
insert_nth(Element,0,L,[Element|L]).
insert_nth(Element,Position,[H|L],[H,NL]) :- M is Position-1, insert_nth(E,M,L,NL).
```

#### Append to list

```
append_list([], L, L).
append_list([H|T],L,[H|R]):- append_list(T,L,R).
```

### Remove from list

#### Remove at nth point

```
delete_nth(0, [ _|T], T).
delete_nth(N, [H|T], [H|R]) :- M is N-1 , delete_nth(M, T, R).
```

#### Delete all occurrences of element:

```
delete_element(_, [ ], [ ]).
delete_element(X, [X|T], R) :- delete_element(X, T, R).
delete_element(X,[Y|T],[Y|T1]) :- X\=Y , delete_element(X, T, T1).
```

### Modify list

#### Replace element in list by its square

```
square([X], [X1]) :- X1 is X * X.
square([X|Y], [X1|Y1]) :- X1 is X * X, square(Y, Y1).
```

#### Reversing list

```
rev([],[]).
rev([H|T], R) :- rev(T,R1), append(R1,[H],R).
```
Essentially stating if we reverse `[H|T]`, we get `rev(T)` catted with `[H]`.

#### Reverse list and concatenate original (uses `rev` from above)

`rev+(L1,L2) :- rev(L1,L3), append(L3,L1,L2).`

#### Reverse list (and any nested lists)

```
rev1([],[]).
rev1(X,X) :- X \= [_|_].
rev1([H|T],L):- rev1(T,RL),rev1(H,H1), append(RL,[H1],L).
```

### Misc list

#### If first element is same as last element, or list has only one element:

```
fela([X]) :-!
fela([X,X]) :-!
fela([X,Y|T]) :- fela([X|Y]).
```

#### Elements of first lit in second list in the same order

(Without using any other function)

```
contains([],[]).
contains([],[_|_]).
contains([X|T1],[X|T2]):- contains(T1,T2).
contains([X|T1],[Y|T2]):- X \= Y, contains([X|T1],T2).
```

#### Success if list contains only 0

```
nullist([0]). OR nullist([0]):-!.
nullist([0|T]):- nullist(T).
```