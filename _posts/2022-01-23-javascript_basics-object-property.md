---
# Required front matter
layout: post # Posts should use the post layout
title: "JavaScript 기초: 객체의 속성" # Post title
date: 2022-01-23 # Publish date in YYYY-MM-DD format

# Recommended front matter
tags: JavaScript # A list of tags
splash_img_source: /assets/img/posts/2022-01-23/doc-title-img.png
# Splash image source, high resolution images with an aspect ratio close to 4:3 recommended
splash_img_caption:

# Optional front matter
updated: 2022-01-23 # Updated date in YYYY-MM-DD format
author:
  name:
pin: false
listed: true # false if this post must NOT be included on the posts page, sitemap, and any of the tag pages, default is true
index: true # When false, <meta name="robots" content="noindex"> is added to the page, default is true
---

> <span class="supplementary-text">**자바스크립트 기초:**
> 자바스크립트의 기초 개념을 정리하는 문서 시리즈입니다. <br>(추후 계속 업데이트될 예정)</span>&nbsp;<br>

<br>

### 객체의 속성에 접근하는 법

---

##### 속성 접근자 (Property Accessors)

**속성 접근자란?**
점 또는 괄호 표기법을 이용해 객체의 속성에 접근할 수 있도록 합니다.

```jsx
object.property;
object["property"];
```

<br>

**자바스크립트의 객체:**

- `key` 와 `value`로 이루어져 있습니다.
- 자바스크립트에서 객체는 속성의 이름을 `key` 값으로 사용하는 **연관 배열**이기도 합니다.<br>
  <span class="supplementary-text">(일반적으로 속성과 구별되어 언급되는 메서드도 실질적으론 호출이 가능한 속성이기 때문. 속성의 값이 함수를 가리키는 레퍼런스라면 해당 속성을 메서드라고 부른다.)</span>

<br>

---

#### **점 표기법**

**속성명은 유효한 식별자**여야 합니다. 즉, 데이터타입이 문자열이어야 합니다.<br>
아래 예제의 경우 `object.$1`은 유효하고 / `object.1`은 식별자가 아님으로 유효하지 않습니다.

```jsx
get = object.property;
object.property = set;
```

<br>

예제) `createElement`라는 이름을 가진 메서드를 `document`라는 객체에서 찾아 호출:

```jsx
document.createElement("pre");
```

<br>

**점 표기법으로 소숫점 없는 숫자 리터럴의 메서드 호출하기**<br>
점이 소숫점으로 인식되지 않도록 주의해야 합니다.

```jsx
(77).toExponential(); // 공백 한 칸 추가하기
// or
(77).toExponential(); // 줄 바꿔 쓰기
// or
(77).toExponential(); // 메서드 괄호로 감싸기
// or
(77).toExponential(); // 점 두 개 사용하기
// or
(77.0).toExponential(); // 소숫점 있는 상태로 만들기
// because 77. === 77.0, no ambiguity
```

<br>

#### **괄호 표기법**<br>

속성명으로 **문자열**이나 **심볼**을 사용할 수 있습니다.<br>
문자열은 유효한 식별자가 아니어도 가능합니다. (공백도 가능)

```jsx
get = object[property_name];
object[property_name] = set;
```

<br>

동일 예제) 대괄호 앞에 공백이 존재:

```jsx
document["createElement"]("pre");
document["createElement"]("pre");
```

<br>

##### **계산된 프로퍼티**

객체 생성 시 객체 리터럴 안의 속성 키가 대괄호`[]`로 둘러싸여 있는 경우를 **계산된 프로퍼티(computed property)**라 부릅니다. <span class="supplementary-text">(ES6에 추가)</span><br>
대괄호로 속성(properties) 이름을 감싸며 **속성명을 동적으로** 만듭니다.<br>
`[]` 안에는 자바스크립트 내장 함수 / 메서드 / 계산식 / 변수를 넣을 수 있습니다.

```jsx
let idx = 0;
let obj = {
  ["name" + ++idx]: idx,
  ["name" + ++idx]: idx,
  ["name" + ++idx]: idx,
};
console.log(obj); // [object Object] {
//   name1: 1,
//   name2: 2,
//   name3: 3
```

<br>

주의: `key` 값의 데이터타입은 반드시 문자열이어야 합니다.

```jsx
console.log(gildong.name);
console.log(gildong["name"]);
gildong["hasHair"] = true;
console.log(gildong.hasHair);
```

<br>
<br>

---

#### 단축 표기법

**단축 표기법(Shorthand notations)**은 ES6에 새롭게 추가된 Object literal notation입니다.<br>
객체의 접근 및 제어를 단순화 시켜준다는 특징이 있습니다.<br>
<span class="supplementary-text">(브라우저와의 호환성 체크 필요)</span>

<br>

##### **단축 속성명**

**단축 속성명(Shorthand property names)**은 미리 선언한 변수들을 나열함으로 `“key: value"` 방식의 객체 속성 표시 방법을 대신해 객체를 생성합니다.<br>
이미 생성된 데이터나 파라미터로 전달받은 데이터들을 재사용할 수 있기 때문에 추가의 객체 리터럴 코드를 작성하지 않아도 된다는 장점이 있습니다.

```jsx
let name = "길동";
let age = 5;
let getName = function () {
  return this.name;
};

let friends = { name, age, getName };
console.log(firends.getName()); // "길동"
```

<br>

##### **단축 메서드명**

**단축 메서드명(Shorthand method names)**은 객체에 메서드를 포함할 경우 `function` 키워드를 생략합니다.<br>
기존 `property_name: function() {}`의 구문을 `property_name() {}` 으로 줄여서 표시합니다.

```jsx
let calc = {
  add(a, b) {
    return a + b;
  },
  multiply(a, b) {
    return a * b;
  },
  subtract(a, b) {
    return a - b;
  },
};
console.log(calc.add(1, 2)); // 3
```

<br>
<br>

---

##### 상황에 맞는 속성 접근법 사용하기

<br>
**점 표기법** `.property_name`<br>
코드를 짜는 순간 key해당하는 값을 불러오고 싶을 때 주로 사용합니다.

**대괄호 표기법** `[”property_name”]`<br>
정확하게 어떤 키가 필요할지 모를 때, 즉 키의 이름이 런타임에서 결정될 때 주로 사용합니다.<br>
**동적으로 키의 값을 받아와야 할 경우** 유용합니다.

<br>

```jsx
const gildong = { name: "gildong", age: 6 };

function printValue(obj, key) {
  console.log(obj.key);
}
printValue(gildong, "name"); // undefined
```

<span class="supplementary-text">key 값이 정의되지 않았기 때문에 undefined가 뜨는 모습.</span>

<br>

```jsx
const gildong = { name: "gildong", age: 6 };

function printValue(obj, key) {
  console.log(obj[key]);
}
printValue(gildong, "name"); // gildong
printValue(gildong, "age"); // 6
```

<span class="supplementary-text">이럴 때 속성 계산명을 사용해주면 객체 생성 이후에 키에 관련된 값을 동적으로 받아올 수 있다.</span>

<br>

---

<span class="supplementary-text">
[출처1](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Property_Accessors) |
[출처2](https://velog.io/@kwonh/ES6-%EB%8B%A8%EC%B6%95%EC%86%8D%EC%84%B1%EB%AA%85-%EA%B3%84%EC%82%B0%EB%90%9C%EC%86%8D%EC%84%B1%EB%AA%85-%EB%B9%84%EA%B5%AC%EC%A1%B0%ED%99%94%ED%95%A0%EB%8B%B9-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B0) |
[출처3](https://velog.io/@hongcoder/%EB%8B%A8%EC%B6%95-%EC%86%8D%EC%84%B1%EB%AA%85-%EB%8B%A8%EC%B6%95-%EB%A9%94%EC%84%9C%EB%93%9C%EB%AA%85-%EA%B3%84%EC%82%B0%EB%90%9C-%EC%86%8D%EC%84%B1%EB%AA%85#:~:text=%EB%8B%A8%EC%B6%95%20%EC%86%8D%EC%84%B1%EB%AA%85%EC%9D%B4%EB%9E%80%20%EA%B0%9D%EC%B2%B4,%ED%95%9C%EB%B2%88%EB%A7%8C%20%ED%91%9C%ED%98%84%ED%95%98%EB%8A%94%20%EB%B0%A9%EC%8B%9D%EC%9D%B4%EB%8B%A4.&text=object3%EC%B2%98%EB%9F%BC%20key%20%EC%99%80%20value%EA%B0%92%EC%9D%84%20%ED%95%9C%EB%B2%88%EB%A7%8C%20%EC%A0%81%EC%96%B4%EC%A4%98%EB%8F%84%20%EB%90%9C%EB%8B%A4.)
</span>
