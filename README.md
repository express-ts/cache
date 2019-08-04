# @express.ts/cache
 A simple in-memory cache for <a href="https://github.com/express-ts/starter">@express.ts</a>

### Installation

    npm install @express.ts/cache --save

### Usage
Test.ts
```typescript
import { Cache } from "@express.ts/cache";

export class Test {

  protected value = Date.now();

  getExecutionTime () {
    return Date.now() - this.value;
  }

  @Cache(1000) // 1s
  getExecutionTimeWithCache () {
    return Date.now() - this.value;
  }

}
```
App.ts
```typescript
import { Test } from "./Test";

const testInstance = new Test();

console.log([ // [ 4, 4 ]
  testInstance.getExecutionTime(),
  testInstance.getExecutionTimeWithCache()
]);

console.log([ // [ 24, 4 ]
  testInstance.getExecutionTime(),
  testInstance.getExecutionTimeWithCache()
]);

setTimeout(() => {
  console.log([ // [ 1038, 1038 ]
    testInstance.getExecutionTime(),
    testInstance.getExecutionTimeWithCache()
  ]);
}, 1001)

```

