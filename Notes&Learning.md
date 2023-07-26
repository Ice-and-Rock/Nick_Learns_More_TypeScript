There are 7 primitive types:

- String
- Boolean
- Null
- Undefined
- Number
- Symbol
- BigInt
  Large type:
- Object

The more informaiton you give TypeScript, the more it can help you.

# Chapter 2
_Type inference_: TypeScript figures out what the type is automatically which can guide you through a project

- you can use the 'any' type to opt out of typescripts strict rules. Be wary, though
- should be used when a variable can change it's type

_An Interface_: allows you to define a type (like an object) then use it throughout your app

When building an interface, you can make certain fields optional using '?'...

~~~
interface InventoryItem {
    displayName: string;
    inventoryType: string;
    readonly trackingNumber: string;
    createDate: Date;
    originalCost?: number;

    // the question mark above and below means they're optional
    addNote?: (note: string) => string;
}
~~~

*An enum*: allows you to define a value with limitied options, such as a drop down menu (with two options)

These are by default assigned a numerical value when typescript is compiled.
If you want a literal value to be taken in, you must define the values in the enum
~~~
enum InventoryItemType {
    Computer = "computer",
    Furniture = "furniture"
}

interface InventoryItem {
    displayName: string;
    inventoryType: InventoryItemType;
}
~~~

*A Literal Type*: This does the same as an enum, but easier beacuse it's done in-line using an '|' (or) syntax
~~~
enum InventoryItemType {
    Computer = "computer",
    Furniture = "furniture"
}

interface InventoryItem {
    displayName: string;
    inventoryType: "computer" | "furniture";
}
~~~

Allowing a variable to be a multiple types
- 'any' type
OR
- Union types
~~~
let origionalCost: number | string;
~~~
~~~
type Cost = number | string;
let origionalCost: Cost = 425;
~~~
Error reporting:
- you can use typeof and if statements to create conditional statements, depening what typeScript wants to give you back...
~~~if (typeof originalCost === "number") {
    let cost: number = originalCost;
} else {
    let x = originalCost;
}
~~~

# Chapter 3

*Classes*
Can be used to create objects with set shapes using:
- constructor to create a new object array
- push to add items
- splice to remove items
- get to view items

convert the class.js file to .ts

all possible properties must be defined at the top of the class for typescript to function properly
~~~
class InventoryStore {
  _categories: Category[] = [];
  _items: InventoryItem[] = [];
  _isInitialized: Promise<boolean>;
}
~~~
remember you can define type of objects using enums or literal types outside of the class...
~~~
interface Category {
  name: string,
  displayName: string,
  subCategories: { name: string, displayName: string }[]
}
~~~

Access Modifiers
Inside a class you can set the types to be visible to three areas: private, protected and public
- private, only visible inside the class
- protected, visitble to members in same class and derived classes
- public, visible to all consumers

You can do this for a few reasons but mostly for keeping data inside classes private (protects sensitive data leaking out without being called in the proper function return eg, persons password or addresses)

~~~
class Person {
  public name: string;
  private age: number;
  protected address: string;

  constructor(name: string, age: number, address: string) {
    this.name = name;
    this.age = age;
    this.address = address;
  }

  public greet() {
    return `Hello, my name is ${this.name}. I am ${this.age} years old.`;
  }
}

const person = new Person("John", 30, "New York");
console.log(person.name);       // Accessible (public)
// console.log(person.age);     // Error - Not accessible (private)
// console.log(person.address); // Error - Not accessible (protected)
console.log(person.greet());    // Accessible (public)
~~~

# Chapter 4
Generics <T> 
Allow you to create reusable components (functions, classes, interfaces) that can work with different types. They provide a way to write flexible and type-safe code by allowing you to specify the type of data that a component will work with when you use it, rather than defining the type directly in the component.

Type Checking Javascript Files 
- You can do this when functions from external components that are being imported throw errors
- Done in the Json file: allowJs: true, checkJs: true.
- You should see typescript adding $ to the beginnings of some lines to check the function contents have the correct types

Adding support for native API's
- Often occur when you are importing API data in async functions
- the data doesn't exisit in the current typescript environment 
- Add "lib" and the types of lib to the Json file 

Adding types for external API's
- Use a type declaration
- the easy way to do this is to create a type object after chekcing JSON object in the console/postman so that typescript knows what to look out for
~~~
// third-party-api.d.ts
declare module "third-party-api" {
  export interface User {
    id: number;
    name: string;
    email: string;
  }}
~~~


