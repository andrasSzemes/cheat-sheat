<style>
.block {
    background-color: #f5f5f5;
    padding: 6px 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px 0px grey;margin:15px 0px;
    padding-bottom: 1px;
    font-size:13px;
    transition: all 1s ease;
    overflow: hidden;
}
code {
    font-size: 12px;
}
.block2 {
    background-color: #fffae7;
    padding: 6px 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px 0px grey;margin:15px 0px;
    padding-bottom: 1px;
    font-size:13px;
    color: #7c1212;
    font-weight: 600
}

.detail .long {
    display: none;
  }

  .detail:hover .short {
    display: none;
  }
  .detail:hover .long {
    display: inline;
  }

  .detail .short {
    background-color: #FFF6E9;
  }
</style>

<div class="block">

TypeScript, a programming language developed by Microsoft, was first made available to the public on October 1, 2012. It was designed by Anders Hejlsberg, who is also known for creating Delphi and C#.

TypeScript is a superset of JavaScript, meaning it extends JavaScript by adding static types. This allows developers to catch errors at compile time rather than runtime, improving code quality and development efficiency. The language also introduces features from modern JavaScript and additional capabilities that are not present in JavaScript, such as interfaces, generics, and namespaces.

The main goals behind the development of TypeScript were to:

- Provide a robust tooling and debugging experience for large-scale JavaScript applications.
- Facilitate the development of complex applications by enabling the use of static types.
- Ensure compatibility with existing JavaScript code and libraries.

TypeScript compiles down to plain JavaScript, ensuring compatibility with all JavaScript environments, including web browsers and Node.js. Since its release, TypeScript has gained significant popularity and is widely used in the development of large-scale applications, particularly in enterprise settings. It is also supported by many popular frameworks and libraries, such as Angular, which has adopted TypeScript as its primary development language.
</div>


<div class="block">

**install**: `npm i typescript -g`  

**compile file**: `tsc main.ts` => main.js  
After you've got the main.js file, it can be included in the html file like before.

For not having to compile the file **all the time**, run the `tsc main.ts -w` command
</div>

<div class="block">

Setup configuration for the project: `tsc --init` => tsconfig.json file  

  - We can specify: rootDir, outDir
  - Can add `"include" : ["src"]` to the first depth of the config object, to not to compile .ts files created in the projekt folder outside of "src". (Otherwise that's the default behaviour)
  - `"noEmitOnError": true` if it's set, then if there's an error highlighted in the code, running the tsc command will not compile the files
    - can be also added to the command instead of the config: `tsc --noEmitOnError`

After setting up the tsconfig.json file, we only have to use the `tsc -w` command.

</div>

Basically we could put simply the previous JS file contents into TS files. We would get warnings about a lot of things, but it could be compiled and it would work just fine.

```ts
let a: number = 12;
let b: string = 'a';
let c: boolean = true;
let d: any = {};
let e: string | number; // union type
```
```ts
let f: string[] = ['a', 'b', 'c'];
let g: (string | number)[] = ['a', 'b', 123];
let h: (string | number | boolean)[] = ['a', 123, true];

let myTuple: [string, number, boolean] = ["a", 2, false];
h = myTuple; // fine
myTuple = h // nope, possible that h does not have exactly 3 elements

myTuple[0] = 1 // nah
myTuple[1] = 1 // sure

const sum = (a: number, b: number) => {
    return a + b;
}


let myObj: object = {};
let myObj2: object = [];  // array is fine for object type too

const exampleObj: {prop1: string, prop2: boolean} = {
    prop1: "a",
    prop2: false
}

type SomeType = {
    name?: string, // optional
    active: boolean,
    union: (string, number)[]
}

const something: SomeType = {
    name: "a",
    active: true,
    union: ["b", 2]
}
something.newProp = true // not gonna work

const something2: SomeType = {
    // name is missing, but no problem
    active: true,
    union: ["c"]
}

const someFunction = (something: SomeType) => {
    // this line is fine
    return `${something.name} ${something.active}`
    // calling a method on a potentially undefined value is a warning..
    return `${something.name.toUpperCase()} ${something.active}`
    // have to make the call optional too
    return `${something.name?.toUpperCase()} ${something.active}`
    // could make an if condition for checking if the name prop is existing or not
    if (something.name) {
        // ...
    }

}

// basically could work the same as SomeType
interface SomeInterface {
    name: string,
    active?: boolean, // optional
    union: (string, number)[]
}
```
```ts
enum Grade {
    U,
    D,
    C,
    B,
    A
}

// "Unlike most TypeScript features, Enums are not type-level addition to JS but something added to the language at runtime."
console.log(Grade.U) // 0, they are actually enumerated

enum OtherGrade {
    U = 3, // 3
    D,     // 4, the rest will follow in order
    C,     // 5
    B,     // 6
    A      // 7
}
```
```ts
// Type Aliases
type stringOrNumber = string | number;
type stringOrNumberArray = (string | number)[];

type SomeType = {
    name?: string,
    active: boolean,
    union: stringOrNumberArray
}


// a difference between type and interface
type UserId = stringOrNumber; // just fine
interface PostId = stringOrNumber; // does not work!
```
```ts
// Literal types
let myName: 'Dave'; // just one value is accepted
myName = 'John' // warning

let userName: 'Dave' | 'John' | 'Amy'; // even can give multiple options
userName = 'John' // fine
```
```ts
// functions
const add = (a: number, b: number): number => {
    return a + b;
}

const logMsg = (message: any): void => {
    console.log(message);
}

let subtract = function(c: number, d: number): number {
    return c - d;
}



type mathFunction = (a: number, b: number) => number;
// doing the same as an interface requires a bit different syntax
interface mathFunction2 {
    (a: number, b: number): number
}
let multiply: mathFunction = function (c,d) {
    return c * d;
}

// optional parameters
const addAll = (a: number, b: number, c: number): number => {
    return a + b + c;
}

const optionalAddAll = (a: number, b: number, c?: number): number => {
    // we have to use a typeguard
    if (typeof c !== 'undefined') {
        return a + b + c;
    }
    return a + b;
}

// default parameter
const sumAll = (a: number, b: number, c: number = 2): number => {
    return a + b + c;
}

// rest parameters
const total = (...nums: number[]): number => {
    return nums.reduce((prev, curr) => prev + curr)
}

total(1,2,3,4) // 10

const prodAll = (factor: number, ...nums: number[]) {
    return nums.map(num => factor * num);
}

prodAll(3.14, 1,2,3,4,5,6,7)



const createError = (errMsg: string): never => {
    throw new Error(errMsg);
}

const infinite = (): never => {
    let i: number = 1;
    while (true) {
        i++;
    }
}



const isNumber = (value: any): boolean => {
    return typeof value === 'number' ? true : false;
}

const numberOrString = (value: number | string): string => {
    if (typeof value === 'string') return 'string'
    if (isNumber(value)) return 'number'
    return new Error('This should never happen!') // without this, we have a warning
}   
```


```ts
type One = string
type Two = string | number
type Three = 'hello'

// convert to more or less specific type
let a: One = 'hello'
let b = a as Two // less specific
let c = b as Three // more specific

// SAME BUT IN REACT IT DOES NOT WORK
let d = <One> 'world'
let e = <string | number> 'world' // assertion for narrowing

// usecase for assertion
// return type is more general, then the variable that will store the value
const addOrConcat = (a: number, b: number, c: 'add' | 'concat'): number | string => {
    if (c === 'add') return a + b;
    return '' + a + b;
}

let myVal: string = addOrConcat(2,2,'concat')               // warning
let myVal: string = addOrConcat(2,2,'concat') as string     // fine
let nextVal: number = addOrConcat(2,2,'concat') as number   // What?
// TS sees no problem - but a string is returned
// mistakes can be made with assertions

let what: unknown           // like any, but you can not use it anywhere
10 as string                // here it will yell at you
(10 as unknown) as string   // and you tricked the system, (two assertions)
```

```ts
// the DOM
const img = document.querySelector('img') // inferred HTMLImageElement | null
const id = document.querySelector("id")   // inferred Element | null

const myImg = document.getElementById("#img") // HTMLElement | null


const img = document.querySelector('img') // inferred HTMLImageElement | null
img.src // warning: Object is possibly 'null'
const img = document.querySelector('img') as HTMLImageElement // we know better, it's there
img.src // fine

// OTHER SOLUTION
const myImg = document.getElementById("#img")!  // non-null assertion
myImg.src // still get warning: property 'src' does not exist on type 'HTMLElement'
const myImg = document.getElementById("#img")! as HTMLImageElement // but now the '!' is not needed
```

___
Classes
```ts
// basic structure
class Coder {
    name: string // needed to exist
    music: string
    age: number
    lang: string

    constructor(name: string, music: string, age: number, lang: string) {
        this.name = name
        this.music = music
        this.age = age
        this.lang = lang
    }
}

// visibility/access modifiers
//     without any declaration, all members are public
//     readonly - once it's assigned, it can not be changed
class Coder2 {

    constructor(
        public readonly name: string,   // after adding modifier, above declaration is not needed.
        public music: string,           // automatically turned into class properties
        private age: number,
        protected lang: string
    ) {
        // no need to manually assign them
    }
}

class Coder3 {
    secondLang: string  // warning for not having an initialisation
    secondLang!: string // this way we say that it's on purpose

    constructor(
        public readonly name: string,
        public music: string,
        private age: number,
        protected lang: string = 'Typescript' // optional parameter
    ) {}

    public getAge() {
        return this.age
    }
}

const Dave = new Coder3('Dave', 'Rock', 42)


class WebDev extends Coder {
    constructor(
        public computer: string,
        name: string,
        music: string,
        age: number // still won't be accessible
    ) {
        super(name, music, age)
        this.computer = computer;
    }

    public getLang() {
        return this.lang
    }
}

const Sara = new WebDev('Mac', 'Sara', 'Lofi', 25)
```

```ts
// implement interface
interface Musician {
    name: string,
    instrument: string,
    play(action: string): string
}

class Guitarist implements Musician {
    name: string
    instrument: string

    constructor(name: string, instrument: string) {
        this.name = name
        this.instrument = instrument
    }

    play(action: string) {
        return ""
    }
}
```

```ts
class Peeps {
    static count: number = 0

    static getCount(): number {
        return Peeps.count
    }

    public id: number

    constructor(public name: string) {
        this.name = name;
        this.ad = ++Peeps.count
    }
}
```

```ts
class Bands {
    private dataState: string[]

    constructor() {
        this.dataState = []
    }

    public get data(): string[] {
        return this.dataState
    }

    public set data(value: string[]): void {
        if (Array.isArray(value) && value.every(el => typeof el === 'string')) {
            this.dataState = value
            return
        } else throw new Error("Param is not an array of strings")
    }
}

const MyBands = new Bands()
MyBands.data = ['a', 'b'] // implicit setter
console.log(MyBands.data) // implicit getter
```




```ts
// Index signatures
//    useful when creating an object, but don't know the exact keys
interface Transaction {
    Apple: number
}

const today: Transaction = {
    Apple: 10
}

console.log(today.Apple)    // 10
console.log(today['Apple']) // 10

const prop = 'Apple'
console.log(today[prop]) // warning: Element implicitly has an 'any' type
                         // because expression of type 'string' can't be used to index 'Transaction'
                         // No index signature with a parameter of type 'string' was found on type 'Transaction'

// solution
interface Transaction {
    [index: string]: number
    // readonly [index: string]: number  // could make unmodifiable like that
}

console.log(today['Banana']) // !no warning, we have to take care of it -- undefined

// could be a bit of both
interface Transaction {
    [index: string]: number // now it does not complain
    Apple: 10               // but has obligation to have this field
}


// other example for same logic
interface Student {
    [key: string]: string | number | number[] | undefined
    name: string
    GPA: number
    classes?: number[]
}

const student: Student = {
    name: 'T'
    GPA: 4
    classes: [100, 200]
}

console.log(student.test) // by product is no warning is given now


// So how other to handle?

interface Student {
    // [key: string]: string | number | number[] | undefined
    name: string
    GPA: number
    classes?: number[]
}

for (const key in student) {
    console.log(`${key}: ${student[key]}`)  // what other option we have besides an index signature?
    console.log(`${key}: ${student[key as keyof Student]}`)
    // keyof creates a uniontype of all the possible value types of the Student interface
    // in this case this means the type: "name" | "GPA" | "classes"
}


// also
const logStudentKey = (student: Student, key: keyof Student): void => {
    console.log("...")
}
logStudentKey(student, 'GPA')



// Does not work with literal types
interface Incomes {
    [key: 'salary']: number // NOPE

}

type Streams = 'salary' | 'bonus' | 'sidehustle'
type Incomes = Record<Streams, number>

// but if there are multiples types for values.. then you can not really separate them
type Incomes2 = Record<Streams, number | string> // meh

const monthlyIncomes: Incomes = {
    salary: 500,
    bonus: 100,
    sidehustle: 250
}

for (const revenue in monthlyIncomes) {
    console.log(monthlyIncomes[revenue]) // same error as before.. missing index signature
    console.log(monthlyIncomes[revenue as keyof Incomes]) // solution as before
}
```

```ts
// Generics

const stringEcho = (arg: string): string => arg
const echo = <T>(arg: T): T => arg

const isObj = <T>(arg: T): boolean => {
    return (typeof arg === 'object' && !Array.isArray(arg) && arg !== null)
}

console.log(isObj(true))
console.log(isObj('John'))
console.log(isObj([1,2,3]))
console.log(isObj({ name: 'a' }))
console.log(isObj(null))


// Example 2

const isTrue = <T>(arg: T): { arg: T, is: boolean } => {
    if (Array.isArray(arg) && !arg.length) {
        return { arg, is: false }
    }

    if (isObj(arg) && !Object.keys(arg as T).length) {
        return { arg, is: false }
    }

    return { arg, is: !!arg }
}

// enhanced
interface BoolCheck<T> {
    value: T,
    is: boolean
}

const checkBoolValue = <T>(arg: T): Boolcheck<T> => {
    if (Array.isArray(arg) && !arg.length) {
        return { value: arg, is: false }
    }

    if (isObj(arg) && !Object.keys(arg as T).length) {
        return { value: arg, is: false }
    }

    return { value: arg, is: !!arg }
}

// Example 3

interface HasID {
    id: number
}

// can narrow down the type that can be passed in
const processUser = <T extends HasID>(user: T): T => {
    // process the user with logic here
    return user
}


// Example 4

const getUsersProperty =  <T extends HasID, K extends keyof T> (users: T[], key: K): T[K][] => {
    return users.map(user[key])
}

getUsersProperty([{id: 1, name: "A"}, {id: 2, name: "B"}], 'name') // ["A", "B"]
// Incorrect usage
const invalid = getUsersProperty([{id: 1, name: "A"}, {id: 2, name: "B"}], 'nonexistent');
// Error: Argument of type '"nonexistent"' is not assignable to parameter of type '"id" | "name"'.




// Example 5
class StateObject<T> {
    private data: T

    constructor(value: T) {
        this.data = value
    }

    get state(): T {
        return this.data
    }

    set state(value: T) {
        this.data = value
    }
}

const store = new StateObject("John")
console.log(store.state)

store.state = "Dave" // no problem
store.state = 12     // after the instantiation TS inferred it should be a string, so NOPE

// give the type specifically
const myState = new StateObject<(string|number|boolean)[]>([15])
myState.state = ['Dave', 42, true] // no prob
```



```ts
// utility types, helpful for common type transformations

// Partial
interface Assignment {
    studentId: string,
    title: string,
    grade: number,
    verified?: boolean
}

// we do not require all of the props
const updateAssignment = (assign: Assignment, propsToUpdate: Partial<Assignment>): Assignement => {
    return {...assign, ...propsToUpdate}
}



// Required
// requires all of the properties
const recordAssignment = (assign: Required<Assignment>): Assignment => {
    // send to database...
    return assign
}



// Readonly
const assignVerified: Readonly<Assignment> = {
    ... assignGraded,
    verified: true
}

assignVerified.grade = 88 // NOPE



// Record
const hexColorMap: Record<string, string> = {
    red: "FF0000",
    green: "00FF00",
    blue: "0000FF"
}

type Students = "Sara" | "Kelly"
type LetterGrades = "A" | "B" | "C" | "D" | "U"

const finalGrades: Record<Students, LetterGrades> = {
    Sara: "B",
    Kelly: "U"
}


interface Grades {
    assign1: number,
    assign2: number
}

const gradeData: Record<Students, Grades> = {
    Sara: { assign1: 85, assign2: 93 },
    Kelly: { assign1: 76, assign2: 15 },
}





// Pick and Omit
type AssignResult = Pick<Assignment, "studentId" | "grade">

const score: AssignResult =  {
    studentId: "k123",
    grade: 85
}

type AssignPreview = Omit<Assignment, "grade" | "verified">

const preview: AssignPreview = {
    studentId: "123",
    title: "Final Project"
}




// Exclude and Extract
//   not working wit interfaces, but with string literal union types
type adjustedGrade = Exclude<LetterGrades, "U">

type highGrades = Extract<LetterGrades, "A" | "B">



// Nonnullable
type AllPossibleGrades = 'Dave' | 'John' | null | undefined
type NamesOnly = NonNullable<AllPossibleGrades>





// ReturnType
const createNewAssign = (title: string, points: number) => { // TS can guess the return type
    return { title, points }
}

type NewAssign = ReturnType<typeof createNewAssign> // { title: string, points: number }
// if we're going to change the code and the type will change also
// we won't have to update the return type this way

const tsAssign: NewAssign = createNewAssign("Utility Types", 100)



// Parameters
type AssignParams = Parameters<typeof createNewAssign> // [title: string, points: number]

const assignArgs: AssignParams = ["Generics", 100]
const tsAssign2: NewAssign = createNewAssign(...assignArgs)




// Awaited - helps us with the ReturnType of a Promise
interface User {
    id: number,
    name: string
}

const fetchUsers = async (): Promise<User[]> => {
    const data = await fetch("https://...")
        .then(res => res.json())
        .catch(err => {
            if (err instanceof Error) console.log(err.message)
        })
    return data
}

type FetchUsersReturnType = ReturnType<typeof fetchUsers>           // Promise<User[]>
type FetchUsersReturnType = Awaited<ReturnType<typeof fetchUsers>>  // User[]
```



npm create vite@latest

```ts
// For me it's interesting that in an interface we can declare "fields" to be implemented
interface Item {
    id: string,
}

// as we could satisfy the requirements like this below
class ListItem implements Item {
    constructor(
        public id: string
    ) {}
}

// this results in that we can access the id like this
const item = new Item("123")
console.log(item.id)

// but as TS uses the get keyword in classes, we can have the same result in a different way
class ListItem implements Item {
    constructor(
        private _id: string
    ) {}

    get id(): string {
        return this._id
    }
}

const item = new Item("123")
console.log(item.id)
// for me it's a but strange after using Java for example to mash up these concepts
```

