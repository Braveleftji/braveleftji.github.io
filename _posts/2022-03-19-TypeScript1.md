---
title: TypeScript 001. JavaScript와 TypeScript
author: 꼬낄라
date: 2022-03-19 18:32:00 -0500
categories: [Coding, TypeScript]
tags: [JaveScript, TypeScript,Dev,Programming]
---
## JavaScript의 짧은 역사 (What is JavaScript? A Brief History)

`JavaScript`는 처음에 브라우저를 위한 스크립팅 언어로 만들어졌다. `JavaScript`가 처음 나왔을 때, 수십 줄 이상의 코드를 작성하는 것은 다소 이례적인 일이었기에 웹 페이지 속 짧은 코드들을 위해 사용할 것으로 여겨졌다고 한다. 때문에, 초기 웹 브라우저들은 수십 줄 이상의 코드를 실행하는데 오래 걸렸는데, 시간이 흘러 JS가 점점 더 유명해지면서, 웹 개발자들은 JS를 이용해 상호작용을 하는 경험을 하기 시작했다고 한다.

웹 브라우저 개발자들은 위와 같이 늘어나는 JS 사용량에 대하여 실행 엔진(동적 컴파일)을 최적화시키고 최적화 된 것을 이용해 할 수 있는 일(API 추가)을 확장하여 웹 개발자가 더 많이 JS를 사용할 수 있게 했다. 현대 웹사이트에서, 브라우저는 수십만 줄의 코드로 구성된 어플리케이션을 자주 실행한다. 이는 정적 페이지의 간단한 네트워크로 시작해서, 모든 종류의 만족스러울만한 `어플리케이션`을 위한 플랫폼으로 성장한 “웹”의 길고 점진적인 성장이다.

이외에도, JS는 node.js를 사용하여 JS 서버들을 구현하는 것처럼, 브라우저 맥락에서 벗어나는 일에 사용하기 충분할 정도로 유명해졌다. “어디서든 작동됨”과 같은 JS의 성질은 교차 플랫폼(cross-platform) 개발을 위한 매력적인 선택지이기도 하다. 오늘날 많은 개발자들은 오직 JavaScript만을 이용하여 전체 스택을 프로그래밍하고 있다!

요약하자면, 우리에게는 빠른 사용을 위해 설계되었으며 수백만 줄의 어플리케이션들을 작성하기 위해 만들어진 완벽한 도구인 JavaScript가 있다. 모든 언어는 각자의 별난 점 - 이상한 점과 놀랄만한 점이 있으며, `JavaScript`의 자랑스럽지만은 않은 시작은 많은 문제를 만들게 되었다. 예를 들어:

-   JavaScript의 동일 연산자는 (==) 인수를 강제로 변환하여(coerces), 예기치 않은 동작을 유발한다:

```javascript
if("" == 0) {
// 참이다! 근데 왜죠??
}
 //error x


if (1 < x < 3) {
// *어떤* x 값이던 참이다!
}
 //error x
```

-   JavaScript는 또한 존재하지 않는 프로퍼티의 접근을 허용한다:

```javascript
const obj = { width: 10, height: 15 };
// 왜 이게 NaN이죠? 철자가 어렵네요!
const area = obj.width * obj.heigth;
//                               ^오타

console.log(area)
//NaN   
// error x
```

---

## TypeScript: 정적 타입 검사자 (TypeScript: A Static Type Checker)

Java 와 같은 몇 언어는 버그가 있는 프로그램을 아예 실행시키지 않는다. 프로그램을 실행시키지 않으면서 코드의 오류를 검출하는 것을 `정적 검사` (컴파일 시) 라고 한다. 어떤 것이 오류인지와 어떤 것이 연산 되는 값에 기인하지 않음을 정하는 것이 정적 타입 검사다.

`정적 타입 검사자`인 TypeScript는 프로그램을 실행시키기 전에 `값의 종류`를 기반으로 프로그램의 오류를 찾는다. 예를 들어, 위의 마지막 예시에 오류가 있는 이유는 obj의 타입 때문이다. 다음은 TypeScript에서 볼 수 있는 오류이다:

```typescript
//@errors: 2551 
const obj = { width: 10, height: 15 };
const area = obj.width \* obj.heigth;
```

#### 타입이 있는 JavaScript의 상위 집합 (A Typed Superset of JavaScript)

그렇다면 TypeScript는 JavaScript와 어떤 관계일까요?

### 구문 (Syntax)

TypeScript는 JS의 구문이 허용되는, JavaScript의 상위 집합 언어이다. 구문은 프로그램을 만들기 위해 코드를 작성하는 방법을 의미한다. 예를 들어, 다음 코드는 )이 없으므로 구문 오류이다:

```typescript
// @errors: 1005
let a = (4
```

TypeScript는 독특한 구문 때문에 JavaScript 코드를 오류로 보지 않는다. 즉, 어떻게 작성돼있는지 모르지만 작동하는 JavaScript 코드를 TypeScript 파일에 넣어도 잘 작동한다.

### 타입 (Types)

그러나 TypeScript는 타입이 있는 상위 집합이다. 위의 `obj.heigth` 오류는 구문 오류가 아닌, 값의 종류(타입)를 잘못 사용해서 생긴 오류이다.

또 다른 예시로, 아래와 같은 JavaScript 코드가 브라우저에서 실행될 때, 다음과 같은 값이 출력될 것이다:

```typescript
console.log(4 / []);
```

구문적으로 옳은(syntactically-legal) 위 코드는 JavaScript에서 `NaN`을 출력한다.

그러나 TypeScript는 배열로 숫자를 나누는 연산이 옳지 않다고 판단하고 오류를 발생시킨다:

```typescript
// @errors: 2363
console.log(4 / []);
```

만약 JavaScript 파일의 코드를 TypeScript 코드로 옮기면, 코드를 어떻게 작성했는지에 따라 `타입 오류`를 볼 수 있다.

### 런타임 특성 (Runtime Behavior)

TypeScript는 JavaScript의 `런타임 특성`을 가진 프로그래밍 언어이다. 예를 들어, JavaScript에서 0으로 나누는 행동은 런타임 예외로 처리하지 않고 Infinity값을 반환한다. 논리적으로, TypeScript는 JavaScript 코드의 런타임 특성을 절대 변화시키지 않는다.

즉 TypeScript가 코드에 타입 오류가 있음을 검출해도, JavaScript 코드를 TypeScript로 이동시키는 것은 같은 방식으로 실행시킬 것을 보장한다

JavaScript와 동일한 런타임 동작을 유지하는 것은 프로그램 작동을 중단시킬 수 있는 미묘한 차이를 걱정하지 않고 두 언어 간에 쉽게 전환할 수 있도록 하기 위한 TypeScript의 기본적인 약속이다.

### 삭제된 타입 (Erased Types)

개략적으로, TypeScript의 컴파일러가 코드 검사를 마치면 타입을 삭제해서 결과적으로 “컴파일된” 코드를 만든다. 즉 코드가 한 번 컴파일되면, 결과로 나온 일반 JS 코드에는 타입 정보가 없다.

타입 정보가 없는 것은 TypeScript가 추론한 타입에 따라 프로그램의 `특성`을 변화시키지 않는다는 의미이다. 결론적으로 컴파일 도중에는 타입 오류가 표출될 수 있지만, 타입 시스템 자체는 프로그램이 실행될 때 작동하는 방식과 관련이 없다.

마지막으로, TypeScript는 추가 런타임 라이브러리를 제공하지 않는다. TypeScript는 프로그램은 JavaScript 프로그램과 같은 표준 라이브러리 (또는 외부 라이브러리)를 사용하므로, TypeScript 관련 프레임워크를 추가로 공부할 필요가 없다.

---

## JavaScript와 TypeScript 학습 (Learning JavaScript and TypeScript)

종종 “JavaScript 또는 TypeScript를 배워야 할까요?”와 같은 질문을 볼 수 있다.

정답은 JavaScript를 배우지 않고선 TypeScript를 배울 수 없다는 것이다! TypeScript는 JavaScript와 구문과 런타임 특성을 공유하므로, JavaScript에서 배운 모든 것들은 동시에 TypeScript를 배울 때 도움이 될 것이다.

Ref. [https://www.typescriptlang.org/ko/docs/handbook/typescript-from-scratch.html](https://www.typescriptlang.org/ko/docs/handbook/typescript-from-scratch.html)(TypeScript)
