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

>1. I wonder what 'array decaying' means, and when it happens.
<p>

    - 배열 붕괴(array decaying)이 무엇을 뜻하는지, 언제 발생하는지가 궁금합니다.

</p>

>2. I wonder if the two variables below are interpreted in the same way.
<p>

    - 아래 두 변수가 같은 방식으로 해석되는 것인지 궁금합니다.

</p>

```c

char(*zippo)[2] = NULL;
char zippo2[4][2];

zippo = (char(*)[2])malloc(sizeof(char[2]) * 4);

```

