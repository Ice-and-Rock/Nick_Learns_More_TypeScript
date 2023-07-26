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

#Chapter 2
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

#Chapter 3
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



