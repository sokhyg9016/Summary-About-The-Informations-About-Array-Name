# Summary-About-The-Informations-About-Array-Name

내가 stack overflow에 올린 질문에 대한 답변들을 살펴보고, 배열이름과 포인터, 또한 배열과 포인터에 관한 궁금했던 점들을 정리해보고, 요약해보자.

| **작성일**       | **키워드**           |  **참고**|
| ------------- |:-------------:|:-------------:| 
| 2019.07.29     | `implicit-conversion` `pointers` `arrays` `c` | `STACK OVERFLOW` |

## what is array decay in c and when it happen?
> [참고] <a href = "https://stackoverflow.com/questions/19441793/when-are-array-names-constants-or-pointers">when-are-array-names-constants-or-pointers</a>
<br>

I am currently studying C language. 
My Questions is here.

>1. 'array decaying' means, and when it happens.
<p>

    - 배열 붕괴(array decaying)이 무엇을 뜻하는지, 언제 발생하는지가 궁금합니다.

</p>

>2. if the two variables below are interpreted in the same way?
<p>

    - 아래 두 변수가 같은 방식으로 해석되는 것인지 궁금합니다.

</p>

```c

char(*zippo)[2] = NULL;
char zippo2[4][2];

zippo = (char(*)[2])malloc(sizeof(char[2]) * 4);

```

나는 이런 식으로 배열 붕괴란 무엇인지, 또한 언제 발생하는지와 위의 코드가 같은 의미를 가지는지를 물었다. 5분이 지나자 답변이 달리기 시작했다.

## Answers
From the C Standard (6.3.2.1 Lvalues, arrays, and function designators)

> [참고] <a href = "http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1256.pdf">C Standard</a>
>>NOTE: When you want to see the document about below quote, open the link and find chaper 6


|3 Except when it is the operand of the sizeof operator or the unary & operator, or is a string literal used to initialize an array, an expression that has type ‘‘array of type’’ is converted to an expression with type ‘‘pointer to type’’ that points to the initial element of the array object and is not an lvalue. If the array object has register storage class, the behavior is undefined.| 
|:---|
<p>
    
    "sizeof"연산자나 단항 & 연산자 또는 배열 초기화에 사용되는 문자열 초기화인 경우에 피연산자로써 
    사용되는 3가지 경우를 제외하고, "배열의 형식"을 가진 식은 배열 객체의 초기 요소를 가리키며
    L-value 가 아닌 포인터로 변환된다.  
    
</p>

즉, 중요한 것은 위에서 말한 3가지 예외의 경우를 제외하고는 ```배열 이름```은 ```&arr[0]```으로 쓴 것과 같은 포인터로 변환되며 ```l-value```가 아니라는 말은 즉, 배열 이름은 결국 **___```non-modifable l-value```___** 라는 뜻이다. 

그러나 ```배열 이름```이 포인터라고 할 수 는 없다. ```배열 이름```은 포인터가 아니며, ```배열``` 또한 포인터가 아니다. 그렇다면 이게 대체 무슨 말인가?

> [참고] <a href = "https://stackoverflow.com/questions/1641957/is-an-array-name-a-pointer">is-an-array-name-a-pointer</a>

|An array is an array and a pointer is a pointer, but in most cases array names are converted to pointers. A term often used is that they **___```decay```___** to pointers.| 
|:---|
<p>

    배열은 배열이고 포인터는 포인터지만 대부분의 경우 배열 이름은 포인터로 변환된다. 
    즉, 배열 이름이 포인터로 암시적인 형 변환(implicit type conversion)을 겪을 뿐이다.
    이러한 변환을 붕괴(decay)라고 한다.

</p>

> [참고] <a href = "https://stackoverflow.com/questions/1461432/what-is-array-decaying/1461466#1461466">what-is-array-decaying</a>

|```Decay``` refers to the ``implicit conversion`` of an expression from an ```array type``` to a ```pointer type```. In most contexts, when the compiler sees an array expression it converts the type of the expression from "N-element array of T" to "pointer to T" and sets the value of the expression to the address of the first element of the array.| 
|:---|
<p>

    붕괴(Decay) 는 표현식을 배열 유형에서 포인터 유형으로 암묵적으로 변환하는 것을 말한다. 
    대부분의 맥락에서, 컴파일러는 배열 식을 볼 때 식의 유형을 "N-요소 배열 of T"에서 "pointer to T"로 변환하고
    식 값을 배열의 첫 번째 요소의 주소로 설정한다.

</p>

이러한 ***```decay```*** 는 앞에서 본 3가지의 예외의 경우를 제외하면 자주 발생하는 현상이다. 즉, 함수로 배열을 넘겨줄 때나 함수의 매개 변수로, 예를 들어
```int a[]```로 쓴 것이 ```int* a```으로 변환되는 것 등이 이러한 예이다.

<br>

| **참고: 이 파트는 의역한 부분이 절반이 넘는다.. 그러니 참고에 나와있는 링크로 가서 직접 보는 것을 추천한다.** |
|:---|

<br>

## 정리

1. ```배열 이름```은 ```수정할 수 없는 L-value``` 값이다
1. 배열 이름은 포인터가 아니며, 배열 또한 포인터가 아니다. (그 반대도 마찬가지이다.)
1. ```붕괴(Decay)``` 는 배열 이름이 몇몇 상황에서 포인터로 ```암시적인 형 변환(implicit type conversion)```을 겪는 현상을 말한다.
1. 배열 붕괴(Array Decay)를 ```Automatic Array Convertion```이라고 말하기도 한다.

## 참고
1. <a href = "https://stackoverflow.com/questions/19441793/when-are-array-names-constants-or-pointers">when-are-array-names-constants-or-pointers</a>
1. <a href = "https://stackoverflow.com/questions/57268963/what-is-array-decay-in-c-and-when-it-happen">what-is-array-decay-in-c-and-when-it-happen</a>
1. <a href = "https://stackoverflow.com/questions/17752978/exceptions-to-array-decaying-into-a-pointer?noredirect=1&lq=1">exceptions-to-array-decaying-into-a-pointerM</a>
1. <a href = "https://stackoverflow.com/questions/1641957/is-an-array-name-a-pointer">is-an-array-name-a-pointer</a>
1. <a href = "https://www.acmicpc.net/board/view/12309">백준 - 질문</a>
