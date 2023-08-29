links: [[020 Languages]]
tags: #TypeScript

------

syntactic superset of JS adds static typing 

benefits: TypeScript uses compile time type checking. which means it checks if the specified types match before running the code, not while running the code

TS runs anywhere JS runs

variable creation `Explicit` and `Implicit`

```TypeScript
let firstName: string = 'Dylan';
```

```TypeScript
let firstName = 'Dylan';
```

```TypeScript
typing objects

const car: { type: string, model: string, year: number } = {  
  type: "Toyota",  
  model: "Corolla",  
  year: 2009  
};
```


Union types are used when a value can be more than a single type
```TypeScript
function printStatusCode(code: string | number) {  
  console.log(`My status code is ${code}.`)  
}  
printStatusCode(404);  
printStatusCode('404');
```

```TypeScript
// the `: number` here specifies that this function returns a number  
function getTime(): number {  
  return new Date().getTime();  
}
```

##### Casting
```TS
let x: unknown = 'hello';  
console.log((x as string).length);
```

```TS
let x: unknown = 'hello';  
console.log((<string>x).length);
```
