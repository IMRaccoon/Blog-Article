깔끔하게 코드를 짠다는 매우 주관적인 생각입니다.

하지만 대부분과 동일하게, 저에게 클린 코드는 _간결_ 하고, _직관적_ 이며, _안전한_ 코드 입니다.

### 즉, **짧고**, **읽기 좋고**, **오류가 나지 않는** 코드입니다.

뭐 당연한 이유겠지만 굳이 이런 코드를 만드는 이유를 하나하나 짚어 보고 넘어 가겠습니다.

#### 1. **짧은 코드**

타인의 코드를 읽는 것은 매우 힘든 일입니다.  
코드에는 그 사람의 성격, 성향이 녹아져 들어갑니다.  
강제로 본인과 맞지 않는 코드를 보는 것은 **지루**하며 **효율이 무척 떨어지는 일**입니다.  
그렇기 때문에 더욱 간결한 코드가 필요한 이유입니다.

#### 2.**읽기 좋은 코드**

읽기 좋은 코드에는 **구조가 한눈에 보이는 것**과 **함수 또는 변수가 어떤 역할을 수행하는 지**가  
타인이 보기에도 명확한 것입니다.  
또한, 엄청 짧은 코드를 만들어서 행복할 순 있겠지만,  
과연 **처음보는 사람이 이 코드를 알아볼 수 있을 지** 생각해 보아야 합니다.

#### 3. **오류가 나지 않는 코드**

**TDD** 방식의 프로그래밍을 합니다. TDD는 **Test-Driven Development**, **테스트 주도 개발**입니다.  
말 그대로, 테스트를 주도하여 개발하는 방법을 이야기 하며,  
다시 말하면 테스트를 먼저 작성한 뒤, 그에 대한 로직을 작성하는 방법입니다.  
일반적으로 본인이 코드를 작성한 뒤에는 무의식적으로 테스트를 간단하게 만들어서 통과하는데 급급하게 됩니다.  
이를 방지하기 위해서 먼저 테스트를 꼼꼼하게 만든 다음 테스트들을 통과시켜주기 위한 개발이 필요합니다.

> TDD 방식의 코딩은 다음에 다뤄보도록 하겠습니다.

<br></br>

## 그럼 깔끔하게 코딩하는 방법 보도록 하겠습니다.

---

사실 저도 클린 코드를 누군가에게 알려줄 정도로 잘하지는 않습니다.

다만 ES6 이후의 함수들로 이전의 단순하던 코드들, 또는 다른 언어에서 생겼던 버릇을 고쳐주기 위함입니다.

```JavaScript
var a = [1, 2, 3, 4, 5];
var sum = 0;
for(let i = 0 ; i < a.length; i++) {
    sum = sum + i;
    // 또는 sum += i;
}
```

지금까지 노말한 Java 또는 C를 배운 뒤, for문을 작성하는 방법입니다.

사실 알고리즘을 제외하고 실제로 개발할 때에는 for문이 전체의 element들을 도는 역할을 합니다.

reduce 함수와 화살표 함수(이하 arrow function)을 활용한다면

```JavaScript
var a = [1, 2, 3, 4, 5];
var sum = a.reduce((prev, cur) => (prev += cur), 0);
```

또는

```JavaScript
var sum = [1, 2, 3, 4, 5].reduce((prev, cur) => (prev += cur), 0);
```

이렇게까지 줄일 수 있습니다.

아래의 방법을 활용한다면 `var a` 같은 의미없는 변수를 선언할 필요 없습니다.

<br></br>

### 줄이는 것이 꼭 좋은 방법만은 아닙니다.

함수는 한 가지 이상의 일을 해서는 안됩니다.

가장 많이 사용하는 것이 매개변수를 flag의 역할을 수행하는 것이죠

```JavaScript
function creatFile(name, temp) {
    if(temp) {
        fs.create(`./${temp}/${name}`);
    } else {
        fs.create(name);
    }
}
```

이런 방식의 함수는 하나의 함수가 두 가지 역할을 수행하는 경우입니다. 번거롭지만

```JavaScript
function createFile(name) {
    fs.create(name);
}

function createTempFile(name, temp) {
    fs.create(`./${temp}/${name}`);
}
```

위의 방법으로 사용하는 것이 이 후, 재사용성이 높고 직관성이 높기 때문입니다.

하지만 저는 저렇게 나누는 것보다 아래의 방식을 더 선호합니다.

```JavaScript
function createFile(name, temp?) {
    if(!!temp) {
        fs.create(`./${temp}/${name}`);
    }
    else {
        fs.create(name);
    }
}

createFile('fileName');
createFile('fileName', 'temp');
```

`temp` 라는 매개변수가 들어왔을 때와 들어오지 않았을 경우, 두 가지 모두

하나의 함수에서 자연스럽게 사용할 수 있기 때문에, 선언하는 함수의 다양성과 독립성을 충족시켜줄 수 있기 때문입니다.

<br></br>

### 사이드 이펙트를 피합시다.

함수가 값을 받아 어떤 일을 수행하거나 값을 반환할 때에 사이드 이펙트가 생깁니다.

그 값이 다른 함수에서 사용될 때에 영항을 끼치면 안됩니다.

예를 들자면

```JavaScript
let name = "IMRaccoon the Developer";

function splitAllName() {
    name = name.split(' ');
}

splitAllName();
console.log(name); // ['IMRaccoon', 'the', 'Developer']
```

물론 실제로 코딩할 때 이런 식으로 하지는 않을 껍니다.

그래도 이를 개선한 사항을 확인하자면

```JavaScript
function splitAllName(targetName) {
    return targetName.split(' ');
}

const name = "IMRaccoon the Developer";
const splited_name = splitAllName(name);

console.log(name);          // 'IMRaccoon the Developer'
console.log(splited_name);  // ['IMRaccoon', 'the', 'Developer']
```

이런 식으로 이 후에 `name` 이라는 변수를 다시 활용하였을 때,

무결성이 보장되는 것이 사이드 이펙트를 최대한 방지할 수 있는 방법입니다.

또한 다른 예시도 존재합니다. 바로 함수 내에 함수를 사용하는 방법입니다.

```JavaScript
const addNewItem = (cart, item) => {
    cart.push({ item, date: Date.new()});
};
```

이와 같이 함수 내에서 `push`라는 함수를 사용하게 된다면 cart 가 직접 변하게 됩니다.

이 때, 사이드 이펙트는 생길 수 있습니다. 따라서 복제를 한 값을 반환하여 입히는 방식을 도입합니다.

```JavaScript
const addNewItem = (cart, item) => {
    return [...cart, { item, date: Date.new() }];
};
```

<br></br>

지금까지 개인적인 주관이 듬뿍 들어간 클린 코드의 개념을 확인했습니다.

하지만 이 글은 전반적으로 새로운 문법을 활용하는 것을 지향하는 내용을 포함하고 있으며,

실질적인 클린 코드는 아래에 정리되어 있는 마크다운 파일을 확인하는 것을 추천합니다.

https://github.com/qkraudghgh/clean-code-javascript-ko
