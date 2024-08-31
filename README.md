<h1> 타입스크립트(1주차)</h1>

* 타입스크립트 소개 및 설치
* 기본타입 설명
* 함수 클래스 인터페이스
* 타입 추론 제네릭
* 실습


<h2>1. 타입스크립트 소개 및 설치</h2>

>타입스크립트는 정적 타입의 컴파일 언어이며 타입스크립트 컴파일러 또는 바벨(Babel)을 통해 자바스크립트 코드로 변환됩니다.  
>코드 작성 단계에서 타입을 체크해 오류를 확인할 수 있고 미리 타입을 결정하기 때문에 실행 속도가 매우 빠르다는 장점이 있습니다.  
>하지만 코드 작성 시 매번 타입을 결정해야 하기 때문에 번거롭고 코드량이 증가하며 컴파일 시간이 오래 걸린다는 단점이 있습니다.  


***  
>>정적 타입 언어
컴파일시 변수 타입이 결정되는 언어
(C c# C++ 자바)  
>>동적 타입 언어
코드를 실행을 할때 알아서 변수 타입 판단
(자바스크립트 파이썬)
***


<h2>2. 기본타입(스트링/넘버/불린/어레이/이넘,튜플....)</h2>


<h3>스트링[string] -> 문자열</h3>  

```  
let str: string = '안녕하세요.';  
```
***

<h3>넘버[number] -> 숫자  </h3>

```
let num: number = 1;  
```
***

<h3>불린[bloolean] ->  True or False </h3> 

```
let inTest : boolean = false;  
```
***

<h3>어레이[array] -> 배열을 통한 집합 </h3> 

```
let arr: number[] = [1,2,3];  


```
***

<h3>이넘[enum] -> 반복적이 사용을 요하는 비슷한 값의 집합  </h3>

```
enum study {str,num,arr}  
let code: study = study.str;  
console.log(code)  
-> str
```
***

<h3> 튜플[tuple] -> 각 변수마다의 타입 및 자리가 고정된 배열 </h3>

```
let myTuple : [number , boolean ,string];

myTuple = [1 , true , "Study good!"]; // OK

myTuple = [ture , 1 , 1000]; // error

```
***

<h3> 애니[any] -> 아무거나 넣을수 있음 </h3> 

```
let str: any = '안녕하세요';  
let num: any = 1;  
let arr: any = ['1주차', 1, true];  
```
***

<h3> 보이드(Void) -> 리턴이 없는 함수</h3>

```
function sayHi() : void {  
    console.log('안녕하세요  1주차 입니다.  ')  
}  

let a : void = null; // 리턴 X 할당가능  
let b : void = undefined; // 리턴 X 할당가능  
```
***


<h2>3. 함수 클래스 인터페이스</h2>

<h3>함수의 기본 적인 선언 방법</h3>

```
function sayWelcome(): void {
  console.log('환영합니다.')
}

sayWelcome();

-> 환영합니다.
```

```
function sumNumber(a1: number, b2: number): number {  
  return a1 + b2;
}

console.log(sumNumber(1,2));

-> 3
```
***
<h3>
클래스  
</h3>

>클래스 기반 객체 지향 언어가 지원하는 접근 제한자(Access modifier) public, private, protected를 지원하며 의미 또한 동일하다.

```
class Person {
  // constructor 위에 선언
  // 클래스 내에 정의된 property(변수)
  
  //접근 제한자 Private(클래스 내부에서만)
  private name: string;
  //접근 제한자 public(내부 외부가능)
  public year: number;
  //접근 제한자 protected(내부 상속 자식)
  protected day: string;

  
  //생성자 생성
  constructor(name: string, year: number,day: string) {
    this.name = name; //
    this.year = year; //
    this.day  = day;
  }
}
```
***

>클래스 접근을 제한하자

```
// 인스턴스 생성(인터페이스는 사용하지못한다.)
const Hanyang = new Person('Student', 2024, 'Sunday');


console.log(Hanyang.name);
//Property 'name' is private and only accessible within class 'Person'.

console.log(Hanyang.year);

console.log(Hanyang.day);
//Property 'day' is protected and only accessible within class 'Person' and its subclasses.



```


***

<h3>인터페이스</h3>  

>자주 사용하는 타입들을 object 형태의 묶음으로 정의해 새로운 타입을 만드는 기능이다.

```
interface User{
    year : number;
    name : string;
}


```
***

변수로서 활용

```
const Hanyang: User = {name:"한양스터티", year: 2024}

//const 상수 변하지 않는값
//let   변수 변화가 되어지는 값
```
***

함수 인자로 활용

```
function getUser(user: User){
    console.log(user);
}  

getUser({name:"Hanyang",year: 2024});
```
***

인터페이스의 확장

```
interface Person {
  name: string;
  year: number;
}

interface Developer extends Person {
  day: string;
}

const Hanyang: Developer = {
  name: "Study",
  year: 2024,
  day: "Sunday"
};

```
***

<h2>4. 타입추론 제네릭</h2>

<h3>
타입추론
</h3>
  

>타입 추론이란 타입스크립트가 코드를 해석해 나가는 동작을 의미한다.

```
let x = 3;
let y = '안녕'

// 따로 X의 타입을 지저을 하지 않더라고 X는 NUMBER 로 간주된다.
// y 는 STRING 으로 간주된다.
```

>변수를 선언하거나 초기화 할대 타입이 추론됩니다.

***
<h3> 제네릭 </h3>

>재사용성이 높은 컴포턴트르 만들대 사용됨
한자기 타입보다 여려가지 타입에서 동작하는 컴포넌트를 생성하는데 사용(독립된 모듈)  

```
function getText(text){
    return text;
}

getText("안녕");
->안녕

getText(10);
->10

getText(true);
->true
```

>제네릭을 넣어서 살펴보겠습니다.  

```
function getText<T>(text: T):T{
    return text;
}
// <> 제네릭 사용 하겠다는 선언
// 함수 사용방법은 다음과 같이 변화합니다.

getText("안녕"); ->  getText<string>("안녕");
->안녕

getText(10); -> getText<number>(10);
->10

getText(true); -> getText<boolean>(true)
->true
```

>함수 뒤에 <> 사용들 해서 내가 사요알 변수의
타입을 알려 줄수 있습니다.
>예를 들어 이름 나이 성별 등등을 받으려고
함수를 만드려면 하나의 함수로 여려가지 형태로 전달을 할수 있습니다.
