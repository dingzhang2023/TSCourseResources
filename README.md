# TS For Developers

### TS Life Cycle

#### Why TS?

-   Type system shape for data, type checks at compile time
-   Generics
-   Advanced classes
-   Decorators
-   Multiple targets - modern JS features, run on old runtimes

#### TS Setup

```bash
npm i -g typescript ts-node @types/node
# execute ts file method 1
ts-node xx.ts
# execute ts file method 2 compile and then use node or browser to execute js files
tsc xx.ts
node xx.js
```

#### TS Config

```bash
# create tsconfig.json
tsc --init
```

#### TS Types

-   Primitive Types

    -   number
    -   string
    -   boolean
    -   symbol
    -   undefined
    -   null

-   tuple

```typescript
let employeeLockerCode: [string, number] = ['John', 345];
employeeLockerCode = ['5', 6];
employeeLockerCode.push(12); // typescript bug
```

-   function

```typescript
function greetMultiple(...names: string[]) {
	names.forEach((name) => {
		greetToConsole(name);
	});
}
```

-   Any and Unknown

> any just disable Type check
> unknown is a **type-safe any**, you need to check the type before using it, **Type Narrowing**

```typescript
function getSalaryFromExternalService(employeeId: number): unknown {
	return JSON.parse('5');
}

let salary = getSalaryFromExternalService(123);

if (typeof salary === 'number') {
	// type narrowing
	salary++;
}
if (typeof salary === 'string') {
	// type narrowing
	salary.includes('$');
}

if (typeof salary === 'string' || typeof salary === 'number') {
	// type narrowing
	salary.valueOf();
}

if (
	salary &&
	typeof salary === 'object' &&
	'history' in salary &&
	Array.isArray(salary.history)
) {
	salary.history.push(12000);
}
```

-   Type Alias
    > Type aliases: define the shape of an object

```typescript
type Position = 'Programmer' | 'HR';

const myPosition: Position = 'Programmer';

type Colleague = {
	name: string;
	age: number;
	position: Position;
	greetBack?: Function;
};
```

-   Export Types

tsconfig.json

```json
// Emit
"declaration": true /** .d.ts files for share types */
```

```typescript
import { randomBytes } from 'crypto';

export type Employee = {
	name: string;
	id: string;
	email: string;
	salary: number;
};

export function createEmployee(employeeName: string, salary: number): Employee {
	return {
		id: generateRandomId(),
		name: employeeName,
		email: `${employeeName}@coolcompany.com`,
		salary: salary,
	};
}
```

```bash
tsc
```
