# TypeScript Documentation

## Table of Contents

1. [Basic Typescript Topics](#1-basic-typescript-topics)

   [1.1 Introduction to Typescript](#11-introduction-to-typescript)

   [1.2 Data Types: Built-in / Basic Types](#12-data-types-built-in--basic-types)

   [1.3 Data Types: User defined types](#13-data-types-user-defined)

   [1.4 tsconfig](#14-tsconfig)

   [1.5 function](#15-function)

2. [Intermediate TypeScript Topics](#2-intermediate-typescript-topics)

   [2.1 Creating types from types](#21-creating-types-from-types)

   [2.2 Narrowing](#22-narrowing)

   [2.3 Type guards](#23-type-guards-example)

   [2.4 DOM Manipulation with typescripts](#24-dom-manipulation-with-typescript)

3. [Advanced TypeScript Topics]()

## 1. Basic Typescript Topics

### 1.1 Introduction to Typescript

What is TypeScript?

- Typescript is a object oriented programmig language based on javascript.
- it is a superset of js
  Why TypeScript?

- JS Check types in run time while typescript add static typing to JS so we can handle errors before running the program. We can handle errors beofre running the program.
- increase readability and code quality
- We can use it React, Vue, popular JS libraray Angular use TypeScript.
- It can be used in both: client and server side.
- Intellisense IDE Support while coding: code completion, content assist and code hinting.

Code Example of Javascript and TypeScript

```js
// index.js
// without typescript
function addNumbers(num1, num2) {
  console.log(num1 + num2);
}

addNumbers(20, 30);
addNumbers(20, "30");

// with typescript
// without typescript
function addNumbers(num1: number, num2: number) {
  console.log(num1 + num2);
}

addNumbers(20, 30); // no error
addNumbers(20, "30"); // error

// without typescript
let x;
x = 20; // correct
x = "anisul"; // correct

// with typescript
let x: number;
x = 20; // correct it must be number
x = "20"; // Not correct
```

How does typescript work?

- first typescript traslate into javascript then browser understand it
- index.ts -> tsc index.ts -> index.js
- Install node & typescript

  ```js
      local installation: npm intsall typescript --save-dev
      Or
      global installation: npm install -g typescript
  ```

- check various versions:

  ```js
    node --version
    npm --version
    tsc --version
  ```

- for run typescipt in node

```js
npm i ts-node-dev --save-dev
ts-node-dev --respawn --transpile-only server.ts
```

### 1.2 Data Types: Built-in / Basic Types

- Any (super type)
  - built in types: number, string, boolean, void, null, undefined, never
  - user-defined types: Arrays, Enums, Classes, interfaces etc.
  - for avoiding typescript in entire file:
    `// @ts-nocheck`

In TypeScript, you can use basic types to specify the type of variables, function parameters, and return values. Here are some of the basic types in TypeScript:

1. **number**: Represents both integer and floating-point numbers.

   ```typescript
   let age: number = 25;
   let price: number = 9.99;
   ```

2. **string**: Represents a sequence of characters.

   ```typescript
   let name: string = "John";
   ```

3. **boolean**: Represents a true or false value.

   ```typescript
   let isDone: boolean = false;
   ```

4. **any**: Represents a dynamic or untyped value. Avoid using this when possible, as it bypasses type checking. if you have no knowledge about the variable type use any type: user input values

   ```typescript
   let data: any = 42;
   data = "Hello";

   let password: any;
   let passwords: any[];
   ```

5. **void**: Represents the absence of a value, typically used as the return type of functions that don't return anything.

   ```typescript
   function logMessage(): void {
     console.log("This is a log message.");
   }
   ```

6. **null** and **undefined**: Represent null and undefined values, respectively.

   ```typescript
   let n: null = null;
   let u: undefined = undefined;
   ```

7. **never**: Represents a value that never occurs, such as a function that throws an error or an infinite loop.

   ```typescript
   function throwError(message: string): never {
     throw new Error(message);
   }
   ```

These basic types provide a foundation for specifying the types of variables and data in TypeScript. You can use them to ensure type safety in your code and catch type-related errors at compile time.

- inferred Typing

  ```js
  let userName = "anis"; // data type inferred as string
  ```

1. **union**: Union Type - more than one type for variable or function parameter. Program - odd/even for number and string to give idea about this union concept.

   ```js
   let userId: string | number;

   // userId = 101; // no error
   // userId = "101"; // no error
   // userId = true; // error

   function userIdDataType(userId: string | number) {
     console.log(typeof userId);
   }

   userIdDataType("123"); // no error
   userIdDataType(123); // no error
   // userIdDataType(true); // error

   const isEven = (num: number | string) => {
     if (typeof num === "number") {
       console.log(typeof num);
       return num % 2 === 0 ? "even" : "odd";
     } else {
       console.log(typeof num);
       return Number(num) % 2 === 0 ? "even" : "odd";
     }
   };

   console.log(isEven(32));
   console.log(isEven("32"));
   ```

2. **object**: Represents any non-primitive value.

   ```typescript
   let person: object = { name: "Alice", age: 30 };

   let user: {
     name: string;
     age: number;
   };

   user = {
     name: "anisul islam",
     age: 32,
   };

   let names: object;
   names = { name1: "anis" };
   console.log(names);

   let users: object[];
   users = [];

   let user1: { userName: string; userId: number };
   user1 = { userName: "anis", userId: 101 };
   users.push(user1);

   let user2: { userName: string; userId: number };
   user2 = { userName: "rabu", userId: 102 };

   users.push(user2);

   for (const key in users) {
     console.log(users[key]["userName"]);
   }
   ```

3. **array**: Represents an array of values of a specific type. 2 ways to declare: `number[]` or `Array<number>`

   ```typescript
   let numbers: number[] = [1, 2, 3, 4, 5];

   // let users = ["anis", "rabu", "pinky"];

   // let users: string[];
   // users = ["anis", "rabu", "pinky"];

   let users: Array<string>;
   users = ["anis", "rabu", "pinky"];

   // for (let index = 0; index < users.length; index++) {
   //   const element = users[index];
   //   console.log(element);
   // }

   // users.forEach((element) => {
   //   console.log(element);
   // });

   users.sort();
   console.log(users);

   users.push("limon");
   console.log(users);

   users.pop();
   console.log(users);

   users.unshift("milton");
   console.log(users);

   users.shift();
   console.log(users);

   // multi-types array
   // let users: (number | string)[];
   // users = [10, "anis", 25, 35, "islam"];
   ```

4. **tuple**: Represents an array with a fixed number of elements, each with a specific type.

   ```typescript
   let employee: [string, number] = ["John Doe", 30];

   let users: [number, String];
   users = [101, "anis"];

   console.log(users);
   console.log(users[0]);
   console.log(users[1]);

   users.push(102, "sakib");
   console.log(users);
   ```

5. **enum**: Represents a set of named constants. no duplicate data.

   ```typescript
   enum Color {
     Red,
     Green,
     Blue,
   }

   let selectedColor: Color = Color.Red;

   // enum example
   // helps us to store constants

   // numeric enum
   enum UserRequest {
     ReadData,
     // ReadData = 2,
     SaveData,
     UpdateData,
   }

   console.log(UserRequest);
   console.log(UserRequest.ReadData);
   console.log(UserRequest.SaveData);

   // string enum
   enum UserRequest {
     ReadData = "READ_DATA",
     // ReadData = 2,
     SaveData = "SAVE_DATA",
     UpdateData = "UPDATE_DATA",
   }

   console.log(UserRequest);
   console.log(UserRequest.ReadData);
   console.log(UserRequest.SaveData);
   console.log(UserRequest["UpdateData"]);

   // Heterogeneous enum
   enum User {
     id = 101,
     name = "anisul",
   }
   ```

6. **Intersection**: In TypeScript, you can use intersection types to combine multiple types into a single type that has all the properties and methods of each type. Intersection types are created using the `&` operator. Here's an example:

   ```typescript
   // Define two types
   type Employee = {
     name: string;
     role: string;
   };

   type Manager = {
     department: string;
     employeesManaged: number;
   };

   // Create an intersection type
   type ManagerWithEmployeeInfo = Employee & Manager;

   // Create an object that conforms to the intersection type
   const manager: ManagerWithEmployeeInfo = {
     name: "Alice",
     role: "Manager",
     department: "HR",
     employeesManaged: 10,
   };

   // Access properties
   console.log(manager.name); // Alice
   console.log(manager.role); // Manager
   console.log(manager.department); // HR
   console.log(manager.employeesManaged); // 10
   ```

   In this example, we define two types: `Employee` and `Manager`. Then, we create an intersection type called `ManagerWithEmployeeInfo` by combining `Employee` and `Manager` using the `&` operator. The resulting type, `ManagerWithEmployeeInfo`, has all the properties of both `Employee` and `Manager`.

   When we create an object (`manager`) that conforms to the `ManagerWithEmployeeInfo` type, it must have all the properties defined in both `Employee` and `Manager`. This allows us to create objects that have a combination of properties from different types, providing flexibility and type safety.

   Intersection types are especially useful when you want to compose types to represent complex objects or data structures in your TypeScript code.

7. **Custom Type**: you can create your own type

   ```js
   type User = { userName: string, userId: number };

   let users: User[];
   users = [];

   let user1: User;
   user1 = { userName: "anis", userId: 101 };
   users.push(user1);

   let user2: User;
   user2 = { userName: "rabu", userId: 102 };
   users.push(user2);

   let user3: User;
   user3 = { userName: "lucky", userId: 103 };
   users.push(user3);

   // console.log(users);

   type RequestType = "GET" | "POST";
   let getRequest: RequestType;
   getRequest = "GET";

   function requestHandler(requestType: RequestType) {
     console.log(requestType);
   }
   requestHandler("GET");
   ```
