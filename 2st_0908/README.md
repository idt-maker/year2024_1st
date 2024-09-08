<h1> **2주차: TypeScript 심화**</h1>



- 모듈 시스템
- 네임스페이스
- 데코레이터
- 타입 가드, 타입 단언
- 실습: TypeScript 프로젝트 설정 및 빌드



<h2>1. 모듈 시스템</h2>

 모듈은 독립 가능한 기능을 말한다.  

  유지보수의 용이성   
  전역 스코프 오염방지  
  재사용성 향상  

  ```
  A.ts file

  const arr = ['H','A','N','G']

  ```  


  ```
  B.ts file

  const arr = ['Y','A','N','G']

  ``` 
  >> 별개의 파일에 똑같은 변수명을 가지고 있으면 타입스크립트에서는 에러를발생을한다.  
  >> 따라서 각 파일에 전역 변수명이 공유 되는 현상을 막기위해 모듈이라는 개면을 사용을 한다.  
  >> B.ts 파일에 expert {}; 을 추가한다면 에러를 없앨수 있다.

  ```
  B.ts file
  export {};
  const arr = ['Y','A','N','G']

  ```


 
  하나의 파일에서 사용되는 형태를 말한다.  

```
const MAX_WEEK = 12;

interface IStudy {
  name: string;
  week: number;
}
 // 클래스 접근제한자 public 클래스로 통한 인터페이스 확장 implements
 // 인터페이스로 초기화(name week) 해주었기에 확장(implements) 클래스에서는 생략
 // implements 한 클래스에 interface 타입이 없다면 에러를 반환한다.
 // extends 키워드는 상속을 위한 개념 (없거나 있거나)
 // implements 정의갑은 모두 필수적으로 타입으로 지정한 메서드 모두 내부에서 재정의가 필요하다.
class Person implements IStudy {
  
  constructor(public name: string, public week: number) {}
  //아래와 같이 타입을 지정해주지 않으면 에러를 밷는다.
  //constructor(public name, public week) {}
   
}

//함수 램던 함수 ceil() 소수점 반올림
function makeRandomCheck(max: number = MAX_WEEK): number {
  return Math.ceil(Math.random() * max);
}

//상수 객체 선언
const makeStudy = (name: string, week: number = makeRandomCheck()) => ({
  name,
  week,
});
```

>>위 코드에서 다른 페이지(타입스크립트 파일) 불러 오려고하면
  
```

const testMakeWeek = (): void => {
  let A: IStudy = makeStudy("HANE");
  let B: IStudy = makeStudy("YANG");
  console.log(A, B);
};

testMakeWeek();

```
>> 불러올수가 없다고 에러를 밷는다.(IStudy /makeStudy )

>> 이방법을 해결하기위해서 export, import 키워드를 사용을한다.
```
export const MAX_WEEK = 12;

export interface IStudy {
  name: string;
  week: number;
}
 // 클래스 접근제한자 public 클래스로 통한 인터페이스 확장 implements
 // 인터페이스로 클래스를 초기화를 해주었기에 확장 클래스에서는 생략

export class Person implements IStudy {
  constructor(public name: string, public week: number) {}
}

//함수 램던 함수 ceil() 소수점 반올림
export function makeRandomCheck(max: number = MAX_WEEK): number {
  return Math.ceil(Math.random() * max);
}

//상수 객체 선언
export  const makeStudy = (name: string, week: number = makeRandomCheck()) => ({
  name,
  week,
});
```
>> 다음과 같이 선언을 하고
```
import { IStudy, makeStudy } from "./파일명";

const testMakeWeek = (): void => {
  let A:  IStudy = makeStudy("HANG");
  let B:  IStudy = makeStudy("YANG");
  console.log(A, B);
};

testMakeWeek();
```
이렇게 한가지의 파일에서 export를 이용을 하면 외부 파일에서 접근을 할수 있는 재사용 할수 있는 코드를 할수 있게 된다.

<h2>2. 네임스페이스</h2>
모듈의 연장선으로 네임스페이스를 통한 구룹화를 통해서 모듈에 접근을 할수 있게도와준다.  

```
// 하나의 파일 내에서 namespace로 내부 모듈을 정의
namespace StudyModule {
  export const MAX_WEEK = 12;

  export interface IStudy {
    name: string;
    week: number;
  }

  export class Person implements IStudy {
    constructor(public name: string, public week: number) {}
  }

  export function makeRandomCheck(max: number = MAX_WEEK): number {
    return Math.ceil(Math.random() * max);
  }
}

// 네임스페이스 내부 요소 사용
const person = new StudyModule.Person('Bob', StudyModule.makeRandomCheck());
console.log(person);
```  


>>네임스페이스는 하나의 파일내에서 논리적 구분이 필요할때 구룹하 하여 사용을 한다.
>>import와 export를 사용하여 모듈을 내보내고 가져온다.  


<h2>3. 데코레이터</h2>

데코레이더 활성화 를 한다.  
데코레이터는 일종의 함수 이다.
데코레이터는 말 그대로 코드 조각을 장식해주는 역할을 하며, 타입스크립트에서는 그 기능을 함수로 구현하는 것이다.


```
// tsconfig.json
{
  "compilerOptions": {
    ...
    "experimentalDecorators": true,
    ...
  }
}
```  

<h3>클래스데코레이터</h3>  

```
// 클래스 데코레이터 정의
function Logger(constructor: Function) {
  console.log(`클래스 ${constructor.name}이(가) 정의되었습니다.`);
}

// 클래스에 데코레이터 적용
@Logger
class Study {
  constructor(public name: string) {
    console.log(`${this.name}가 생성되었습니다.`);
  }
}

const Univ = new Study('HANCYANG');
// 콘솔 출력:
// 클래스 Study이(가) 정의되었습니다.(데코레이션)
// Univ가 생성되었습니다.
```  

>> 즉 @Logger 이 부분에서 클래스의 생성자 함수 인자를 받아서 클래스가 >> 적용이 댈대 마다 콘솔에 로그를 출력합니다.

<h3>메서드데코레이터  </h3>

```
// 메서드 데코레이터 정의
function LogMethod(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Method ${propertyKey}이(가) 호출되었습니다.`);
    console.log(`인자들: ${args}`);
    const result = originalMethod.apply(this, args);
    console.log(`결과: ${result}`);
    return result;
  };
}

// 클래스 정의
class Calculator {
  @LogMethod
  add(a: number, b: number): number {
    return a + b;
  }
}

const calc = new Calculator();
calc.add(2, 3);
// 콘솔 출력:
// Method add이(가) 호출되었습니다.
// 인자들: 2,3
// 결과: 5
```  
>> 메서드를 호출할대마다 메서드 이름과 인자값을 로그로 출력합니다.

<h3>속성데코레이터</h3>   
 
```
// 속성 데코레이터 정의
function LogProperty(target: any, propertyKey: string) {
  let value = target[propertyKey];

  const getter = () => {
    console.log(`속성 ${propertyKey}의 값을 읽습니다: ${value}`);
    return value;
  };

  const setter = (newValue: any) => {
    console.log(`속성 ${propertyKey}의 값을 설정합니다: ${newValue}`);
    value = newValue;
  };

  Object.defineProperty(target, propertyKey, {
    get: getter,
    set: setter,
    enumerable: true,
    configurable: true,
  });
}

// 클래스 정의
class User {
  @LogProperty
  public name: string = 'Alice';
}

const user = new User();
user.name = 'Bob';
//log 속성 name의 값을 설정합니다: Bob
console.log(user.name);
//log 속성 name의 값을 읽습니다: Bob

```  

>> LogProperty는 속성 데코레이터로, name 속성에 접근할 때마다 속성 값을 읽거나 설정하는 시점에 로그를 출력합니다.  
>> setter와 getter를 통해 속성의 읽기/쓰기를 감지하고 처리할 수 있습니다.


<h3>매개변수데코레이터</h3>    

```
// 매개변수 데코레이터 정의
function LogParameter(target: any, propertyKey: string, parameterIndex: number) {
  console.log(`${propertyKey} 메서드의 ${parameterIndex}번째 매개변수에 데코레이터가 적용되었습니다.`);
}

// 클래스 정의
class Greeter {
  greet(@LogParameter message: string) {
    console.log(`안녕하세요, ${message}`);
  }
}

const greeter = new Greeter();
greeter.greet('한양');
// 콘솔 출력:
// greet 메서드의 0번째 매개변수에 데코레이터가 적용되었습니다.
// 안녕하세요, 한양

```
>>greet 메서드의 첫 번째 매개변수에 @LogParameter 데코레이터가 적용되어, 해당 매개변수에 대해 로그를 남깁니다.


>>>클래스 데코레이터: 클래스를 감싸서 추가 동작을 부여.  
>>>메서드 데코레이터: 메서드 호출 전후에 특정 로직을 삽입.  
>>>속성 데코레이터: 클래스 속성에 대한 접근을 감시.  
>>>매개변수 데코레이터: 메서드 매개변수에 대한 추가 정보나 동작을 설정.  
>>>데코레이터는 코드의 가독성과 재사용성을 높이고, 클래스나 메서드에 쉽게 추가 기능을 적용할 수 있게 도와줍니다.  



<h2>3. 타입 가드, 타입 단언</h2>

<h3>typeof를 사용한 타입 가드</h3>  

```
function printValue(value: string | number) {
  if (typeof value === 'string') {
    console.log(`문자열: ${value.toUpperCase()}`);
  } else {
    console.log(`숫자: ${value.toFixed(2)}`);
  }
}

```
>>typeof value === 'string' 조건문 안에서 value는 문자열 타입으로 좁혀지게 된다.
>>if (typeof value === 'string') 조건문을 사용하여 value가 문자열인지 확인합니다.
typeof 연산자는 런타임에 변수의 타입을 검사할 때 사용됩니다.
>>이 함수는 입력된 값이 문자열인지 숫자인지에 따라 다른 처리를 수행하여 결과를 출력합니다. 타입 가드(typeof 연산자)를 사용함으로써 TypeScript는 value의 구체적인 타입을 알고, 해당 타입에서 사용할 수 있는 메서드(toUpperCase, toFixed)를 안전하게 호출할 수 있습니다.
  
<h3>instanceof를 사용한 타입 가드</h3>  

```
class Dog {
  bark() {
    console.log('멍멍');
  }
}

class Cat {
  meow() {
    console.log('야옹');
  }
}

function makeSound(animal: Dog | Cat) {
  if (animal instanceof Dog) {
    animal.bark();
  } else {
    animal.meow();
  }
}

```  

>>animal instanceof Dog를 통해 **animal이 Dog 클래스의 인스턴스인지** 확인하고, 그 안에서 **bark 메서드를 안전하게 호출**할 수 있습니다.


<h3>사용자 정의 타입 가드</h3>    

```
interface Fish {
  swim: () => void;
}

interface Bird {
  fly: () => void;
}

function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;

//**매개변수 pet**은 Fish 또는 Bird 타입을 가질 수 있습니다.
//**pet is Fish**라는 반환 타입은 TypeScript에서 사용자 정의 타입 가드를 정의하는 방식입니다.
//만약 swim 메서드가 undefined가 아니라면, pet은 Fish 타입이라고 판단할 수 있습니다.
}

function move(pet: Fish | Bird) {
  if (isFish(pet)) {
    pet.swim();
  } else {
    pet.fly();
  }
}
//move 함수는 pet이 Fish 또는 Bird일 수 있으므로, 타입 가드를 통해 타입을 좁혀주고 있습니다.
//if (isFish(pet))에서 isFish 함수가 true를 반환하면, TypeScript는 pet이 Fish 타입임을 알고 swim() 메서드를 호출할 수 있습니다.
//반대로 isFish(pet)가 false를 반환하면 pet이 Bird 타입이라고 간주하고, fly() 메서드를 호출합니다.
```  

>>isFish(pet): pet is Fish는 pet이 Fish 타입인지를 확인하는 사용자 정의 타입 가드입니다.(타입의 좁히는 방법)
함수 내에서 isFish(pet)가 참일 경우, pet은 Fish 타입으로 좁혀지며 swim 메서드를 안전하게 호출할 수 있습니다.
>>타입 가드는 TypeScript에서 변수의 타입을 좁히는 방법을 제공하는 기능입니다. 이 코드는 Fish와 Bird라는 두 가지 인터페이스와 함께, isFish라는 사용자 정의 타입 가드를 사용하여 pet이 Fish인지 Bird인지 구분하는 구조입니다.
>>사용자 정의 타입 가드는 typeof, instanceof로 처리하기 힘든 복잡한 타입 확인을 가능하게 하며, 코드의 타입 안정성을 높여줍니다.

  
  <h3>기본적인 타입 단언 사용</h3>  

  ```
let someValue: unknown = "hello world";

// 컴파일러는 someValue가 unknown 타입이므로 문자열 메서드를 사용할 수 없음
// let strLength: number = someValue.length; // 오류 발생

// 타입 단언을 통해 문자열로 간주
let strLength: number = (someValue as string).length;

console.log(strLength); // 출력: 11

  ```

  >>someValue는 unknown 타입으로 선언되었기 때문에 문자열 메서드 length를 사용할 수 없습니다.
someValue as string을 통해 someValue가 문자열이라고 컴파일러에 알려주고, 그 후에 문자열 메서드를 사용할 수 있습니다.


 <h3>as와 <Type> 문법의 차이(타입단언)</h3>    
 >>타입 단언(type assertion)**을 통해 컴파일러에게 특정 값이 지정된 타입임을 명시적으로 알려줄 수 있습니다.  
 >> 이를 두 가지 방법으로 표현할 수 있는데, 바로 as 문법과 <Type> 문법입니다.  
 >> 이 두 방식은 기능적으로는 동일하지만, 일부 차이가 있습니다.
    
 ```
 let someValue: any = "hello";

// as 문법
let strLengthAs: number = (someValue as string).length;

//설명: someValue가 string 타입임을 컴파일러에 알려주는 문법입니다.
//someValue가 현재 any 타입이지만, as string을 통해 컴파일러가 someValue를 string으로 인식하게 되어 .length를 사용할 수 있습니다.


// <Type> 문법
let strLengthAngle: number = (<string>someValue).length;

//위의 as 문법과 동일하게, someValue가 string 타입임을 컴파일러에 알려주는 방식입니다.
//<string>을 통해 someValue의 타입을 string으로 단언하고 .length를 사용할 수 있습니다.
 ```

 >>as 문법: (value as Type) 형태로 사용되며, JSX가 포함된 파일에서 안전합니다.
 >><Type> 문법: <Type>value 형태로 사용되며, 일반 TypeScript 파일에서 사용하기 좋습니다.  


>>타입 단언을 사용할 때 주의할 점
>>타입 단언은 개발자가 타입을 더 잘 알고 있다는 가정 하에 사용됩니다.
>>따라서, 타입 단언을 남용하면 런타임 에러를 일으킬 가능성이 있습니다.
>>타입 단언은 컴파일러의 타입 검사를 무시하기 때문에, 실제로 타입이 맞지 않더라도 컴파일 오류 없이 실행될 수 있습니다.
>> 따라서 가능한 한 안전한 범위 내에서 사용해야 합니다.  

```
let value: any = "hello";
let num: number = value as number; // 이 코드에서는 런타임 에러 발생 가능

```
