# partialRight

미리 인자를 뒤에서부터 제공한 함수를 만들어요.

[partial](./partial.md)와 동작이 비슷한데요, 인자를 뒤에서부터 제공한다는 차이가 있어요.

Symbol 타입의 `partialRight.placeholder`를 쓰면, 미리 제공한 인자가 사용될 위치를 결정할 수 있어요.

함수의 `length` 프로퍼티는 설정하지 않아요.

## 인터페이스

```typescript
function partialRight<F extends (...args: any[] => any)>(func: F, ...partialArgs: any[]): (...args: any[]) => ReturnType<F>;

namespace partialRight {
  placeholder: symbol;
}
```

### 파라미터

- `func` (`F`): 미리 인자를 제공할 함수.
- `partialArgs` (`any[]`, 선택): 미리 제공될 인자.

### 반환 값

(`(...args: any[]) => ReturnType<F>`): 미리 인자가 제공된 함수.

## 예시

```typescript
import { partialRight } from 'es-toolkit/function';

function greet(greeting, name) {
  return greeting + ' ' + name;
}

const greetFred = partialRight(greet, 'fred');
greetFred('hi');
// => 'hi fred'

// Partially applied with placeholders.
const sayHelloTo = partialRight(greet, 'hello', partialRight.placeholder);
sayHelloTo('fred');
// => 'hello fred'
```
