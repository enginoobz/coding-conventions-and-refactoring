<a name="0"></a>  
# Table of Contents
1. [Abbreviation](#abbreviation)
1. [Naming](#naming)
2. [Commenting](#commenting)
3. [Preference](#preference)
4. [Shorthand](#shorthand)
5. [Git](#git)
6. [Architecture](#architecture)

<a name="abbreviation"></a>  
### I - Abbreviation
> Should be **universally accepted**, provide **good result of shortening**, used for naming & commenting
* **addr** address - **app** application
* **bg** background - **btn** button
* **char** character - **col** column - **coord** coordinate
* **db** database - **dest** destination - **dir** directory
* **len** length
* **msg** message
* **num** number
* **obj** object
* **pwd** password - **param** parameter - **pic** picture - **pos** position
* **str** string - **src** source
* **val** value - **var** variable

<a name="naming"></a>  
# II - Naming
[⬆ To the top](#0)

### 1 - Variable
+ **Element/HTMLElement** ```e prefix```: *eBtn*
+ **NodeListOf\<Element>** ```es prefix```: *esBtn* (questionable?)
+ **JQuery\<HTMLElement>** ```$ prefix```: *$btn* (questionable?)
+ **Boolean** ```{tobe}+{noun}+{adj/verb-ed}```: *wasBtnClicked*, *areBtnsGreen*
+ **Private class member** ```_ prefix```: *_id* (questionable?)

### 2 - Others
+ **Constant** (primitive type && project/file/class-scoped) ```SNAKE_CASE | All caps```: *BTN_SELECTOR*
+ **Function/variable/constant** (reference type || function-scoped) ```camelCase```: *disableBtn()*
+ **Class/struct/record** ```PascalCase```: *CoolBtn*
+ **Interface** ```PascalCase | I prefix```: *IClickable*
+ **Enum** ```PascalCase | Singular```: *BtnState {Clicked, Focus, Hover, Active, Disabled}*
+ **Event** ```camelCase | on+{noun}+{ordinal}+{action}```: *onBtnClick*, *onBtn1stClick*
+ **CSS class** ```BEM```: *hero__btn--round* ([reference](https://sparkbox.com/foundry/bem_by_example))

<a name="commenting"></a>  
# III - Commenting
[⬆ To the top](#0)
### 1 - Document
+ **Variable**: same line
```
public string cookie; // this meta tag has been deprecated in M63
```
+ **Output**

Result of single statement: same line
```
console.log('foobar') // expected output: foobar
```
Result of block of statements: below
```
const a = 'foo'
const b = 'bar
console.log(a + b)
// expected output: foobar
```
+ **Function/block**: above 
```
// this does...
function fooBar(){}
```
+ **Ordered procedure**: above each line w/ cardinal numbers	
```
// 1. Create an interface representing a document in MongoDB
inteface User { name: string...
// 2. Create a Schema corresponding to the document interface
const schema = new Schema<User>({...
// 3...
```
+ **Mixed procedure**: above the procedure + mark according line w/ cardinal numbers	

```
/**
 * Main content containers
 * 1. Make the container full-width with a maximum width
 * 2. Center it in the viewport
 * 3. Leave some space on the edges, especially valuable on small screens
 */
.container {
  max-width: $max-width; /* 1 */
  margin-left: auto; /* 2 */
  margin-right: auto; /* 2 */
  padding-left: 20px; /* 3 */
  padding-right: 20px; /* 3 */
  width: 100%; /* 1 */
}
```
  
### 2 - Task
+ **TODO** general tasks
+ **FIX**
+ **REMOVE** the code is used for reference later and removed when becoming unneccesary.
+ **ADHOC** temporary code needed to be replaced by more elegant solutions.
+ **UTIL** utility/helper method should be moved into a dedicated file.
+ **REFACTOR** - **DRY** - **PARAMETERIZE**
+ **SPECIFIC** the code inside a general framework/library to solve problems for only a specific project, should be moved into that very project
  
### 3 - Section
> Use **upper case** to search by matched case in files containing many categorizes, components, etc. (esp CSS file)
+ **Categorize** containing multiple components
```
/*-------------------------
      BASIC COMPONENTS
-------------------------*/

///////////////////////////
//    BASIC COMPONENTS
```
+ **Component**
```
/* BUTTON */
```

<a name="preference"></a>  
# IV - Preference
[⬆ To the top](#0)
> Alternative ways of doing stuffs but help improving **code readability & clarity**
+ ~~Enum~~ => **Union types** ([reference](https://fettblog.eu/tidy-typescript-avoid-enums/?fbclid=IwAR18SiWtUFai4gEY4B6rm2nSGYfR54Yw3bitrkl4Ph9z72qwM_8kbOUYhX8)) *[TS]*
+ ~~Equality operator (==)~~ => **Strict equality operator** (===) *[TS]*
+ ~~Promise/callback chaining~~ => **async-await** *[ES6]*
+ ~~try-finally~~ => **using** *[C#]*
+ **Object initializer/builder** [C#]*
+ **Object destructuring** *[TS/JS]*
+ **Named arguments** *[PHP, Kotlin]*
+ **Guard clause/assert/precondition**
+ ~~String~~ => **StringBuffer** for string appending *[Java, C#]*
+ ~~String concatenation operator (+)~~ => **String interpolation/template literals** *[TS/JS, Kotlin, PHP]*
```
console.log("Sum of " + a + " and " + b + " is " + (a + b))
// preference
console.log(`Sum of ${a} and ${b} is ${a + b}`)
```

<a name="shorthand"></a>  
# V - Shorthand
[⬆ To the top](#0)
> Recommend to utilize following features if available in the using language for **code brevity**
### 1 - Declaration & Initialization
+ W/ **Nullish coalescing operator (??)** *[C#, PHP, ES11]*
```
result = (a !== null && a !== undefined) ? a : b;
// shorthand
result = a ?? b
```
+ W/ **short circuit evaluation** *[most languages]*
```
result = (a !== null && a !== undefined) ? a : b;
// shorthand
result = a || b
```
+ **Logical nullish assigment operator (??=)** *[TS/JS]*
```
a ?? (a = b)
// shorthand
a ??= b
```
+ **Multiple variable declaration** [ES, C#, Java]
```
let a;
let b;
let c = 3;
// shorthand
let a, b, c=3;
```
+ **Implicit typing (var)**: for long named type *[C#]*
```
AReallyReallyLooooongClass instance = new AReallyReallyLooooongClass();
// shorthand
var instance = new AReallyReallyLooooongClass();
```
+ **Concise new (new())** *[C#9]* 
```
ExampleClass instance = new ExampleClass();
// shorthand
ExampleClass instance = new();
```
  
### 2 - Control Flow
+ **Ternary operator (? :)** *[most languages]*
```
if (a > b) {
    result = x;
}
else {
    result = y;
}
// shorthand
result = a > b ? x : y;
```
+ Conditional w/ **truthy/falsy values** *[TS/JS, Groovy, Perl, PHP, Python, Ruby]*
```
if(typeof a !== "undefined" && typeof b !== "null" && typeof c !== "NaN" && d !== "" && array.length !== 0)
// shorthand
if(a && b && c && d && array.length)
```
+ Conditional w/ **short circuit evaluation** *[most languages]*
```
if(isHungry) {
  code()
}
// shorthand
isHungry && code()
```
  
### 3 - Class, Object, Function
+ **Constructor shorthand/property promotion** *[TS, PHP8]*
```
class User {
  private name: string;
  private age: number;
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}
// shorthand
class User {
  constructor(
    private name: string,
    private age: number
  ) {}
}
```
+ **Object property value shorthand** *[ES6]*
```
let cat = 'Miaow';
let dog = 'Woof';
let bird = 'Peet peet';

var myPets = {
  cat: cat,
  dog: dog,
  bird: bird
}
//shorthand
let myPets = {
  cat,
  dog,
  bird
}
```
+ **Lambda expression/Arrow function (=>)** *[Java8, ES6, Dart]*
```
function getSum(a: number, b: number) {
  return a + b
}
// shorthand
const getSum = (a: number, b: number) => (a + b)
```

### 4 - Mathematics
+ **Exponent power** *[ES]*
```
const power = Math.pow(4, 3);
// shorthand 
const power = 4**3;
```
+ **Floor rounding** *[ES]*
```
const floor = Math.floor(6.8);
// shorthand 
const floor = ~~6.8;
```
+ **Decimal base exponents** *[ES]*
```
10000000
// shorthand
1e7
```

### 5 - Conversion
+ String to number *[ES]*
```
const num1 = parseInt("100");
const num2 =  parseFloat("100.01");
// shorthand
const num1 = +"100";
const num2 =  +"100.01";
```

### Others
+ **Spaceship/three-way comparison operator (<=>)** *[C++, Groovy, Kotlin, Perl, PHP, Ruby]*
```
$users = ['branko', 'ivana', 'luka', 'ivano'];

usort($users, function ($a, $b) {
  return ($a < $b) ? -1 : (($a > $b) ? 1 : 0);
});
// shorthand
usort($users, function ($a, $b) {
  return $a <=> $b;
});
```
+ **Spread operator (...)** [ES6]

For joining arrays:
```
const odd = [1, 3, 5];
const nums = [2 ,4 , 6].concat(odd);
// shorthand
const odd = [1, 3, 5 ];
const nums = [2 ,4 , 6, ...odd];
```
  
For cloning array:
```
const arr = [1, 2, 3, 4];
const arr2 = arr.slice()
// shorthand
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
```

<a name="git"></a>  
# VI - Git
[⬆ To the top](#0)
+ **Repo name** ```kebab-case | All lower``` (avoid lowerscore _ which seem bad for URL)
  
### Commit message
+ **Initial commit** first commit of the project involving common/familiar setup.
+ **[Exp]** experimenting, trying out a feature. This code can be used for reference later and removed when getting familiar (marked with // REMOVE).
+ **[Refactor]** refactoring code, removing unnecesary code/comments, reorganinzing code/files, etc.
+ **[Fix]**
+ **[Test]**
+ **[Doc]**

<a name="architecture"></a>  
# VII - Architecture
[⬆ To the top](#0)
> Standard approaches to structure & organize code files
+ **SASS** ```7-1 pattern``` ([reference](https://www.learnhowtoprogram.com/user-interfaces/building-layouts-preprocessors/7-1-sass-architecture))
+ **TS & NodeJS** ([reference](https://github.com/microsoft/TypeScript-Node-Starter))
