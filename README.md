# mathematic-note

# Mathematic for working programmer DAY1

TBC

-------
# Mathematic for working programmer DAY2

## **computation by pattern matching(stateless) and term rewriting**
Find pattern -> Define the rules <br>

## **probelm solving with pure function**
Pure function is purely mathematic function just map things to things <br>

> Are you functional thinking ?

**2 layer of algorithm**
1. **function** High level for human comunication <br>
2. **step** as Low level for machine state <br>


**Step**
1. validate given string is a palindrome
2. generate palindorme from string
3. determine how many unique word are given sentence
4. determine if two string are anagram

> ** palindorme คือ อูยองอู

**Example** : A &rarr; B <br>
`"this bat" "this cat" "this rat"` <br>

> **Solution** <br>
A &rarr; A1 &rarr; B1 &rarr; B <br>
A &rarr; A1 as **step1** <br>
B1 &rarr; B as **step2**

```
B1 -> B to count word
exactly we have -> [this, cat, bat, rat] 

A1 -> B1 to unique
result -> [this, bat, this, cat, this, rat]

A -> A1
["this bat", "this cat", "this rat"]
```
**Live Coding** in Haskell<br>

**Example**
```
> swap (A, B) this is pattern
> (B, A)
```
**Let get started!**

```
> count ["this", "bat", "cat", "rat"] => 4

> unique ["this, "bat", "cat", "rat"] => ["this, "bat", "cat", "rat"]
> count (unique ["this, "bat", "cat", "rat"]) => 4 
state B1 -> B is now complete by above code!
```

```
> split  "this bat this cat this rat" = ["this", "bat","this", "cat", "this","rat"]
```
so then
```
>  count (unique (split  "this bat this cat this rat")) = 4
```
then define function

countUniqueWord -> count . unique . split <br>
**count**
```
> count = length
> count "this" = 4
```
**unique** we would like to sort or order or grouping
```
> unique = nub
> words " this is a cat"
> countUniqueWord -> count . unique . words
> countUniqueWord " this is a bat this is a cat this is a rat"
> 6
```

**Warp-up to haskell thing**

```
> code demo.hs


import Data.List
countUniqueWord = count . unique .  words
where
    count = length
    unique = nub
```

> support : มี user บางคน มีปัญหา <br>
me : id user อะไรครับ (this is exactly) <br>

**Recap** <br>
Functional programming consist of **probelm solving** with pure function and **computation** of pattern and rewriting <br>

But why does it matter ??? <br>
Introducing <br>
> "The worst pice of code you'll ever encounter" <br>

```
= the code that we don't know what it solving

> if( a == 'a' || a == 'e'  || a == 'i' || a == 'o' || a == 'u') {
    count ++
}
เราเดาได้ว่า เช็คสระ แต่ถามว่าถูกไหม aren't vowels which this is low-level?

replace this with 

if(isVowels(a)){
    count++;
}

boolean isVowels(string a) {
    a.toLowerCase();
    return a == 'a' || a == 'e' || a == 'i' || a == 'i' || a == 'o' || a == 'u';
}

isVowels(a) function can be determine what we would like to solve and it is high level code to comunication


why we lowercase a in isVowels()
because we need to specific char 1 to 1 checking, so when we need to test is vowel we can easily assert isVowels(A) == 1

```

**Functional thinking lead to**
> 1. Readable
> 2. Reasonable
> 3. Testable
> 4. Well-factorized

Why does pure function matter ?
> "Simple to reason with it"
```
Suppose we have a function 
f: int -> int

f will result only int

** Avoid hidden dependencies 
```


**Side effects** 
example
```
double monte(int n) {
    int a =  random()
    int b = random()

    //call random() something -> which it works using side effect, it depend on external seed value


    //logging 
    logger.info("a =", a, "b = ", b)

    return a * b

}
```
> Can we tell any of that w/ just this? <br>
> **No way**

Purler function version
```
double pure_monte(a, b) {
    return a * b
}

```
***Why pure function is matter ?***

- ยกตัวอย่างการดึงค่าจาก cahce 
ใน monte() จะไม่เกิด log ถ้าดึง value จาก cahce

- แล้วถ้าcode depend on random number มึงจะ assert ยังไงวะครับ

- error logs: monte จะ reproduce ยังไง

--------

## **Sets, Functions and Categories**

### **Sets**

> **"Everything is a member of a set"**

eg. boolean [true, false] , int [(n, n-1), 0,(n, n+1)] and so on ...

 But in *computer programming* **SET usaually mean data structure or specific container**

**- Types** <br>
Saying *e is Type T === e is element of T* <br>
 - type inference
 ```
 > type true
 > boolean

 > type 'A'
 > char

 //type is equal to set

 ```

 Do functions have type ?
 ```
> type not
> boolean -> boolean 
//means set of boolean to boolean 
//we call this function type



bool function() {
 
} 
//boolean is type of return value not function type
 ```


 ### **Functions**

> f: Domain -> Co-domain

Domain -> Co-Domain


```
> not (not true)
will be
> not false

```
it chan-able if domain differ to co-domain
```
> not (not ( not ( not false)))
```
but long function chain would be leadious to write, **espeacially the "()"**

**- Unary function** <br>
function with one arguments

```
> true || false
> false
```
> is it an operator ? **No**

**- 4 kinds of function notation**
1. Prefix
2. Infix 
3. Postfix
4. Uniquly specific

> "programming languages" can express mathematical function into formal form <br>
e.g. double sin(double a, double b)

**to prove it's' function, we can check type**

**- Curries function**
> "Every function only takes one arguement"
revisit function from high school


this is only valid function form <br>
f: Domain -> Codomain

ง่ายๆคือ Domain หรือ Codomain contain มากกว่า 1 function
เช่น 
```
int [5, 7, 11, 17]
char [a]

int x char [5a 7a 11a 17a] 
this is tuple


//Domain can contain int x char (tuple)

> type (True, 'a')
> (True, 'a') :: Bool -> Char
```
เราเรียกว่า Cartersian product/ simply product

พอกลับมาดู function ที่เราเขียนในโค้ด

เช่น
```
login("username", "password")
```
("username", "password") มันก็คือ tuple ตัวนึง


แต่ถ้ามันอ่าน Tuple ไม่ได้ ทำไง <br>
**Example** <br>
ต้องเป็น Curry


```
add: aInt -> bInt -> cInt

มันก็คือ
aInt -> bInt -> cInt

ยุบรวม
add': aInt -> (bInt -> cInt)
```

```
> type add
> add :: int -> int -> int
> type add 5
> add 5 :: int -> int
> add 5 7
// มันคือ function add 5 ที่รับ argument 7 
// (add 5) 7
> 12

```

```
> type filter
> filter :: (char -> bool) -> string -> string
```

OOP in functional perspective

```
> void doWork() {...
```
Reason this . . . <br>
**No, We can't** <br>
these are not showed in doWork()
1. type
2. value
3. name 

void -> void is not a functions

**OOP (Alan kay definition)** should have fixed above probelm
> "System of biological cells, communicateing with chemical substance"

biological cells become object
chemical substance become message

and so, object will response the message with its methods

ตัวอย่างที่ใกล้เคียงสุดคือ
http request ไปหา internal server แต่ไม่ใช่ระดับของ OOP มันเป็นระดับ architecture 

```
dog.bark()
```
มีกี่ arguement ?
> one <br>

in OOP language -> object.method(arg) ***which equivalent*** to method(object, arg)

ดังนั้น [1,2,3,4].filter(isEven) ก็คือ<br>    
```
> filter([1,2,3,4], isEven)
> filter([int], [int -> bool])
```
which call ***Higher-order function***

**meme**
```
ซัก :: ผ้าใส่แล้ว -> ผักซักแล้ว
ตาก :: ผ้าซักแล้ว -> ผ้าแห้ง
รีด :: ผ้าแห้ง -> ผ้าเรียบ
เก็บ :: ผ้าเรียบ -> ผ้าในตู้

"ผ้ากองนี้.ซัก().ตาก().รีด().เก็บ() ด้วยนะคะ" = map(เก็บ.รีด.ตาก.ซัก)[ผ้ากองนี้]
```
**Recap curried function**  <br>
1. All functions take one arguement and can be transfom from Cartersian
2. Basically function constructor
3. Partially apply exist function
4. Applied argrument will be cloesed argument inside function frozen from any change 

> We call this "Closure" <br>


***Let create a function***
```
catById: catId -> Cat

> List[catId]domain -> List[cat] codomain
```
start with db connector
```
> getCatFormDB :: DB -> catID -> Cat
> catById = getCatFormDB(myDB)
> type catById
> catById :: catId -> cat
```
what about API

```
> getCatFormAPI :: API -> catID -> Cat
> catById = getCatFormAPI(request)
> type catById
> catById :: catId -> cat
```

generalize this

```
> catById(DB, 17)
> catById(API, 18)
> catById(Mock, 19)

> catById :: (datasource -> id) -> cat
```

**- Generic function** <br>
domain restriction
example
```
> type filter
> filter :: (a->bool)-> a -> a

> type filter isDigit 
//isDigit :: char-> bool
> filter :: (char) -> char
```


**map** <br>
mini quiz
```
> aaabbc => 3a2b1c
> map(count, char) :: (count->char) -> char

> aaa => '3a'
> 'A':(show 3)
> "A3"
> reverse $ 'A':(show 3)
> "3A"
> reverse $ head 'AAA':(show (length "AAA"))
> compressOne $ = reverse $ head 'AAA':(show (length "AAA"))
> "3A"

what if "AAABBCCAA"
> type group
> group :: Eq a => [a] -> [[a]]

> "AAABBCCAA"
> group it
> ["AAA", "BB", "CC", "AA"]
> map compressOne it
> ["3A", "2B", "2C", "2A"]
> concat it
> "3A2B2C2A"
```



**- List comprehension**


set comprehension
```
A = {a | a ∈ N}
```
list comprehension
```
A = [a | a <- N]
```

**- Recursive** <br>
break it down 
you will see the same probelm

> Key to solve Recursion:
find the way to solve (n-1) -> (n)

> "if function can solve sub probelm it also can solve super probelm"

zip

** Popular recursion probelm**
1. prime number <br>
2 3 4 5 6 7 8 9 10 11 ... 100

```
start with 2  if member of list can be divided with current number we pop it out

3/2 = 1 do nothing
4/2 = 0  pop 4
and then continue to start with 3 and so on ...
```

2. permutation <br>
abc -> abc acb bac  bca cab cba

start with small probelm
ab -> ba 

abc -> a[bc] a[cb] 
**permute bc with a**
and so on ... 

```
permute :: (Eq a) -> [a] -> [[a]]
permute [] = [[]]
permute xs = [x:ys | x <- xs, ys <- permute (delete x xs)]
```

3. tower of hanoi


```
hanoi :: Int -> [(Int, Int)]
hanoi n = hanoi' n 1 2 3 
hanoi' 0 _ _ _ =[]
hanoi' n beg tmp dest = tops_to_tmp 

```


