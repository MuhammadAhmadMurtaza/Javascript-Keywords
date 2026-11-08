<div align="center">

# 🧠 JavaScript Fundamentals: `var`, `let` & `const`

**A hands-on practice file comparing the three ways to declare a variable in JavaScript: scope, hoisting, redeclaration, and mutability**

</div>

---

## 📖 About This Project

This is my first JavaScript practice project. It is a tiny HTML page that loads one script, `script.js`. The script has **no visible output on the page**. Every example prints to the **browser console**, so the project is about reading what the code does and what it prints.

The goal is to understand how `var`, `let`, and `const` differ, and to know which one to reach for by default.

No frameworks, no libraries, no build tools. Just HTML and JavaScript.

---

## 📑 Table of Contents

1. [Project Structure](#-project-structure)
2. [The Three Keywords at a Glance](#-the-three-keywords-at-a-glance)
3. [Part 1: `var`](#-part-1-var)
4. [Part 2: `let`](#-part-2-let)
5. [Part 3: `const`](#-part-3-const)
6. [Expected Console Output](#-expected-console-output)
7. [Errors You Can Trigger on Purpose](#-errors-you-can-trigger-on-purpose)
8. [Known Gaps & Improvements](#-known-gaps--improvements)
9. [Try It Yourself](#-try-it-yourself)
10. [How to Run](#-how-to-run)
11. [Cheat Sheet](#-cheat-sheet)
12. [Key Takeaways](#-key-takeaways)
13. [Roadmap](#-roadmap)

---

## 📂 Project Structure

```
js-fundamentals/
│
└── 01-variables/
    ├── index.html     # blank page that loads the script
    └── script.js      # all the var / let / const examples
```

<table>
  <tr>
    <th>File</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><code>index.html</code></td>
    <td>A minimal page. Its only job is to load <code>script.js</code> with <code>&lt;script src="script.js"&gt;&lt;/script&gt;</code> at the end of <code>&lt;body&gt;</code>.</td>
  </tr>
  <tr>
    <td><code>script.js</code></td>
    <td>Fifteen small examples, grouped into <code>var</code>, <code>let</code> and <code>const</code>. Each one prints its result with <code>console.log()</code>.</td>
  </tr>
</table>

> 💡 Rename the folder to match your own layout. The page looks empty because everything prints to the console, not the page.

---

## ⚖️ The Three Keywords at a Glance

<table>
  <tr>
    <th></th>
    <th><code>var</code></th>
    <th><code>let</code></th>
    <th><code>const</code></th>
  </tr>
  <tr>
    <td><b>Scope</b></td>
    <td>Function scope</td>
    <td>Block scope</td>
    <td>Block scope</td>
  </tr>
  <tr>
    <td><b>Redeclare in the same scope</b></td>
    <td align="center">✅ Allowed</td>
    <td align="center">❌ SyntaxError</td>
    <td align="center">❌ SyntaxError</td>
  </tr>
  <tr>
    <td><b>Reassign the value</b></td>
    <td align="center">✅ Yes</td>
    <td align="center">✅ Yes</td>
    <td align="center">❌ TypeError</td>
  </tr>
  <tr>
    <td><b>Must be initialized when declared</b></td>
    <td align="center">No</td>
    <td align="center">No</td>
    <td align="center">✅ Yes</td>
  </tr>
  <tr>
    <td><b>Hoisted?</b></td>
    <td>Yes, initialized as <code>undefined</code></td>
    <td>Yes, but unusable until declared (TDZ)</td>
    <td>Yes, but unusable until declared (TDZ)</td>
  </tr>
  <tr>
    <td><b>Use before declaration</b></td>
    <td><code>undefined</code></td>
    <td>ReferenceError</td>
    <td>ReferenceError</td>
  </tr>
  <tr>
    <td><b>Top-level in a browser script</b></td>
    <td>Becomes a <code>window</code> property</td>
    <td>Does not</td>
    <td>Does not</td>
  </tr>
  <tr>
    <td><b>When to use</b></td>
    <td>Avoid in new code</td>
    <td>Values that change</td>
    <td><b>Default choice</b></td>
  </tr>
</table>

---

## 📦 Part 1: `var`

The original way to declare variables. It works, but several of its behaviors cause bugs.

<table>
  <tr>
    <th>#</th>
    <th>Example</th>
    <th>What it shows</th>
  </tr>
  <tr>
    <td align="center">1</td>
    <td><b>Basic declaration</b></td>
    <td><code>var name = "Ahmad"</code> declares and prints a string.</td>
  </tr>
  <tr>
    <td align="center">2</td>
    <td><b>Redeclaring is allowed</b></td>
    <td><code>var city = "Lahore"</code> followed by <code>var city = "Karachi"</code> raises no error. It prints <code>Karachi</code>. In a big file this can overwrite a variable by accident.</td>
  </tr>
  <tr>
    <td align="center">3</td>
    <td><b>Hoisting</b></td>
    <td><code>console.log(age)</code> comes <b>before</b> <code>var age = 25</code> and prints <code>undefined</code>, not an error.</td>
  </tr>
  <tr>
    <td align="center">4</td>
    <td><b>Ignores block scope</b></td>
    <td><code>var x = 10</code> inside an <code>if</code> block is still visible outside the block.</td>
  </tr>
  <tr>
    <td align="center">5</td>
    <td><b>Function scope</b></td>
    <td><code>var msg</code> inside <code>test()</code> exists only inside that function.</td>
  </tr>
</table>

### 🧪 Code Highlight

```js
// 2. Redeclaring is allowed (can cause bugs)
var city = "Lahore";
var city = "Karachi";
console.log(city);        // Karachi

// 3. Hoisting: usable before declaration (gives undefined)
console.log(age);         // undefined
var age = 25;

// 4. Ignores block scope
if (true) {
  var x = 10;
}
```

### 🧠 What Hoisting Really Does

JavaScript reads the whole scope first and **moves the declaration to the top**, but not the value. Your code behaves as if it were written like this:

```js
var age;                  // declaration moved to the top, value is undefined
console.log(age);         // undefined
age = 25;                 // the assignment stays where you wrote it
```

### 🌍 Global `var` Becomes a `window` Property

In a browser, a top-level `var` is attached to the global `window` object:

```js
var name = "Ahmad";
console.log(window.name);   // "Ahmad"
```

`name` is also a **built-in** property of `window` (it holds the window's name and always stores text), so reusing it can behave oddly. A name like `userName` avoids the problem. Top-level `let` and `const` do **not** attach to `window`.

---

## 🔄 Part 2: `let`

The modern way to declare a variable **whose value will change**.

<table>
  <tr>
    <th>#</th>
    <th>Example</th>
    <th>What it shows</th>
  </tr>
  <tr>
    <td align="center">1</td>
    <td><b>Basic update</b></td>
    <td><code>let score = 0; score = 10;</code> prints <code>10</code>.</td>
  </tr>
  <tr>
    <td align="center">2</td>
    <td><b>Block scope</b></td>
    <td><code>let y = 5</code> exists only inside the <code>{ }</code> of the <code>if</code>.</td>
  </tr>
  <tr>
    <td align="center">3</td>
    <td><b>No redeclaring</b></td>
    <td><code>let color = "blue"</code> a second time would be an error. Reassigning with <code>color = "blue"</code> is fine.</td>
  </tr>
  <tr>
    <td align="center">4</td>
    <td><b>Loop counter</b></td>
    <td><code>for (let i = 0; i &lt;= 3; i++)</code> prints <code>0, 1, 2, 3</code>. The <code>i</code> exists only inside the loop.</td>
  </tr>
  <tr>
    <td align="center">5</td>
    <td><b>A counter that changes</b></td>
    <td><code>count++</code> then <code>count += 5</code> takes it from <code>0</code> to <code>1</code> to <code>6</code>.</td>
  </tr>
</table>

### 🧪 Code Highlight

```js
// 2. Block scope
if (true) {
  let y = 5;
  console.log(y);         // 5
}
// console.log(y);        // would throw: ReferenceError

// 5. Counter that changes
let count = 0;
count++;                  // 1
count += 5;               // 6
console.log(count);       // 6
```

### ⏳ The Temporal Dead Zone

`let` (and `const`) **are** hoisted, but they cannot be used until the line that declares them runs. The gap between the start of the scope and that line is the "temporal dead zone".

```js
console.log(score);       // ReferenceError: Cannot access 'score' before initialization
let score = 0;
```

This is **safer than `var`**, because you get a loud error instead of a quiet `undefined`.

---

## 🔒 Part 3: `const`

For values that should **not be reassigned**. It is the best default choice.

<table>
  <tr>
    <th>#</th>
    <th>Example</th>
    <th>What it shows</th>
  </tr>
  <tr>
    <td align="center">1</td>
    <td><b>Fixed value</b></td>
    <td><code>const pi = 3.14159</code> stays the same for the whole program.</td>
  </tr>
  <tr>
    <td align="center">2</td>
    <td><b>Reassigning errors</b></td>
    <td><code>country = "India"</code> would throw an error, so that line is commented out.</td>
  </tr>
  <tr>
    <td align="center">3</td>
    <td><b>Must be initialized</b></td>
    <td><code>const z;</code> alone is a SyntaxError. It needs a value: <code>const z = 100</code>.</td>
  </tr>
  <tr>
    <td align="center">4</td>
    <td><b>Arrays</b></td>
    <td><code>fruits.push("Banana")</code> is allowed. The array's <b>contents</b> can change.</td>
  </tr>
  <tr>
    <td align="center">5</td>
    <td><b>Objects</b></td>
    <td><code>student.marks = 95</code> is allowed. An object's <b>properties</b> can change.</td>
  </tr>
</table>

### 🧪 Code Highlight

```js
// 4. Arrays: contents can change, the variable can't be reassigned
const fruits = ["Apple", "Mango"];
fruits.push("Banana");              // allowed
console.log(fruits);                // ["Apple", "Mango", "Banana"]

// 5. Objects: properties can change
const student = { name: "Ali", marks: 80 };
student.marks = 95;                 // allowed
console.log(student);               // { name: "Ali", marks: 95 }
```

### 🧠 The Big Idea: `const` Locks the Variable, Not the Value

<table>
  <tr>
    <th>Action</th>
    <th>Allowed with <code>const</code>?</th>
    <th>Why</th>
  </tr>
  <tr>
    <td><code>fruits.push("Banana")</code></td>
    <td align="center">✅ Yes</td>
    <td>The variable still points to the same array. Only the array's contents changed.</td>
  </tr>
  <tr>
    <td><code>student.marks = 95</code></td>
    <td align="center">✅ Yes</td>
    <td>The variable still points to the same object.</td>
  </tr>
  <tr>
    <td><code>fruits = ["Kiwi"]</code></td>
    <td align="center">❌ No</td>
    <td>That points the variable at a <b>new</b> array, which <code>const</code> forbids.</td>
  </tr>
  <tr>
    <td><code>student = { name: "Sara" }</code></td>
    <td align="center">❌ No</td>
    <td>Same reason: reassignment.</td>
  </tr>
</table>

To also stop an object's properties from changing, use `Object.freeze()` (a shallow freeze, so nested objects can still change):

```js
const settings = Object.freeze({ theme: "dark" });
settings.theme = "light";           // silently ignored (throws in strict mode)
console.log(settings.theme);        // "dark"
```

---

## 🖥️ Expected Console Output

Open the console and you should see these values, in this order:

<table>
  <tr>
    <th>#</th>
    <th>Printed by</th>
    <th>Output</th>
  </tr>
  <tr><td align="center">1</td><td><code>var name</code></td><td><code>Ahmad</code></td></tr>
  <tr><td align="center">2</td><td><code>var city</code></td><td><code>Karachi</code></td></tr>
  <tr><td align="center">3</td><td><code>var age</code> (hoisting)</td><td><code>undefined</code></td></tr>
  <tr><td align="center">4</td><td><code>test()</code></td><td><code>Inside Function</code></td></tr>
  <tr><td align="center">5</td><td><code>let score</code></td><td><code>10</code></td></tr>
  <tr><td align="center">6</td><td><code>let y</code></td><td><code>5</code></td></tr>
  <tr><td align="center">7</td><td><code>let color</code></td><td><code>blue</code></td></tr>
  <tr><td align="center">8</td><td><code>for</code> loop</td><td><code>0</code>, <code>1</code>, <code>2</code>, <code>3</code> (four lines)</td></tr>
  <tr><td align="center">9</td><td><code>let count</code></td><td><code>6</code></td></tr>
  <tr><td align="center">10</td><td><code>const pi</code></td><td><code>3.14159</code></td></tr>
  <tr><td align="center">11</td><td><code>const country</code></td><td><code>Pakistan</code></td></tr>
  <tr><td align="center">12</td><td><code>const z</code></td><td><code>100</code></td></tr>
  <tr><td align="center">13</td><td><code>const fruits</code></td><td><code>["Apple", "Mango", "Banana"]</code></td></tr>
  <tr><td align="center">14</td><td><code>const student</code></td><td><code>{ name: "Ali", marks: 95 }</code></td></tr>
</table>

---

## 💥 Errors You Can Trigger on Purpose

Uncomment these lines one at a time to see each error. They fail in **different ways**, which matters.

<table>
  <tr>
    <th>Code</th>
    <th>Error</th>
    <th>When it happens</th>
    <th>Effect on the rest of the file</th>
  </tr>
  <tr>
    <td><code>let color = "blue";</code> (second time)</td>
    <td><code>SyntaxError: Identifier 'color' has already been declared</code></td>
    <td><b>Before</b> the script runs (parse time)</td>
    <td>🚫 <b>Nothing runs.</b> No output at all.</td>
  </tr>
  <tr>
    <td><code>const z;</code></td>
    <td><code>SyntaxError: Missing initializer in const declaration</code></td>
    <td><b>Before</b> the script runs (parse time)</td>
    <td>🚫 <b>Nothing runs.</b> No output at all.</td>
  </tr>
  <tr>
    <td><code>country = "India";</code></td>
    <td><code>TypeError: Assignment to constant variable.</code></td>
    <td><b>While</b> the script runs</td>
    <td>Everything <b>above</b> that line already ran. Everything below it does not.</td>
  </tr>
  <tr>
    <td><code>console.log(msg)</code> outside <code>test()</code></td>
    <td><code>ReferenceError: msg is not defined</code></td>
    <td><b>While</b> the script runs</td>
    <td>Everything above already ran.</td>
  </tr>
  <tr>
    <td><code>console.log(y)</code> outside the <code>if</code> block</td>
    <td><code>ReferenceError: y is not defined</code></td>
    <td><b>While</b> the script runs</td>
    <td>Everything above already ran.</td>
  </tr>
</table>

> 💡 **Why the difference?** Syntax errors are found when the browser first **reads** the file, before it runs a single line. Runtime errors happen only when execution reaches that line. This is why a single typo can make the whole page "do nothing".

---

## 🔍 Known Gaps & Improvements

Some of the demos describe a behavior in a comment but never actually **prove** it. These small additions make each point visible.

<details>
<summary><b>1. 🧱 Prove that <code>var</code> ignores block scope</b></summary>

<br>

`var x = 10` is declared inside the `if`, but `x` is never printed afterward.

```js
if (true) {
  var x = 10;
}
console.log(x);     // 10  <- still visible outside the block!
```

</details>

<details>
<summary><b>2. 🔒 Prove that <code>let</code> and function-scoped <code>var</code> stay inside</b></summary>

<br>

Neither `y` nor `msg` is ever logged outside its scope. Wrapping the failing line in `try...catch` lets you show the error without stopping the script:

```js
try {
  console.log(y);               // outside the if block
} catch (e) {
  console.log(e.message);       // "y is not defined"
}

try {
  console.log(msg);             // outside the function
} catch (e) {
  console.log(e.message);       // "msg is not defined"
}
```

</details>

<details>
<summary><b>3. ⏳ Add a temporal dead zone demo</b></summary>

<br>

Hoisting is only shown for `var`. Add the contrast for `let`:

```js
try {
  console.log(level);           // let is hoisted but not usable yet
} catch (e) {
  console.log(e.message);       // "Cannot access 'level' before initialization"
}
let level = 1;
```

</details>

<details>
<summary><b>4. 🏷️ Rename <code>name</code></b></summary>

<br>

At the top level of a browser script, `var name` writes to the built-in `window.name`. Use `userName` (or any other name) to avoid the clash.

</details>

<details>
<summary><b>5. 🪧 Small clean-ups</b></summary>

<br>

<table>
  <tr>
    <th>Issue</th>
    <th>Fix</th>
  </tr>
  <tr>
    <td>The HTML <code>&lt;title&gt;</code> is "Document"</td>
    <td>Rename it, for example "JS Variables".</td>
  </tr>
  <tr>
    <td>The page is blank, so it's unclear that anything happened</td>
    <td>Add a line such as <code>&lt;p&gt;Open the console (F12) to see the output.&lt;/p&gt;</code>.</td>
  </tr>
  <tr>
    <td>Typo "Declarartion" in a comment</td>
    <td>Change it to "Declaration".</td>
  </tr>
  <tr>
    <td>Add <code>"use strict";</code> at the top</td>
    <td>Turns some silent mistakes into real errors, such as writing to a frozen object.</td>
  </tr>
</table>

</details>

---

## 🔬 Try It Yourself

<details>
<summary><b>Click to expand the experiment steps</b></summary>

<br>

1. Open the page, press `F12`, and go to the **Console** tab. Match the output against the [expected output table](#-expected-console-output).
2. **Break it with a runtime error.** Uncomment `country = "India";` and notice that the lines above it still print.
3. **Break it with a syntax error.** Uncomment `const z;` (and remove `const z = 100;`) and notice that the console shows **nothing but the error**.
4. **Redeclare a `let`.** Uncomment `let color = "blue";` and watch the whole file refuse to run.
5. **The classic loop test.** Run this and compare:

```js
for (var i = 0; i <= 3; i++) {
  setTimeout(() => console.log("var:", i), 0);   // prints 4, four times
}

for (let j = 0; j <= 3; j++) {
  setTimeout(() => console.log("let:", j), 0);   // prints 0, 1, 2, 3
}
```

Every `var` callback shares **one** variable, which is `4` by the time they run. Each `let` iteration gets its **own** copy.

6. **Freeze an object.** Wrap `student` in `Object.freeze()` and see that `student.marks = 95` no longer changes it.
7. **Inspect `window`.** In the console, type `window.city` and `window.score`. Only the `var` variable shows up.

</details>

---

## 🚀 How to Run

No installation needed for the browser version.

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git

# 2. Move into the project
cd <your-repo-name>/01-variables

# 3. Open the page in your browser
open index.html      # macOS
start index.html     # Windows
xdg-open index.html  # Linux
```

Then open DevTools (`F12`, or `Ctrl+Shift+J` / `Cmd+Option+J`) and choose the **Console** tab.

**Run it with Node.js instead (no browser):**

```bash
node script.js
```

> ℹ️ In Node, a top-level `var` stays inside the file's own module scope instead of becoming a global, so the `window` examples only apply in the browser.

💡 **Tip:** Use the VS Code **Live Server** extension to reload automatically when you save.

---

## 📚 Cheat Sheet

| Situation | Use |
|---|---|
| A value that never gets reassigned | `const` |
| A value that will change (counters, totals, flags) | `let` |
| Arrays and objects you will modify but not replace | `const` |
| Loop counters | `let` |
| Reading older code that uses `var` | Understand it, but don't write new `var` |
| An object that must not change at all | `const` + `Object.freeze()` |

**Rule of thumb:** start with `const`. Change it to `let` only if the code needs to reassign the variable.

---

## 🎓 Key Takeaways

<table>
  <tr>
    <td>✅</td>
    <td><code>var</code> is function scoped, <code>let</code> and <code>const</code> are block scoped.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td><code>var</code> allows redeclaration and gives <code>undefined</code> when used early, which can hide bugs.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td><code>let</code> and <code>const</code> throw an error if used before they are declared, which catches mistakes early.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td><code>const</code> locks the <b>variable</b>, not the <b>contents</b> of an array or object.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Syntax errors stop the whole file before it runs. Runtime errors stop it only from that line onward.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>A top-level <code>var</code> becomes a <code>window</code> property in the browser, but <code>let</code> and <code>const</code> do not.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Default to <code>const</code>, use <code>let</code> when you must reassign, and avoid <code>var</code>.</td>
  </tr>
</table>

---

## 🗺️ Roadmap

- [x] `var`: redeclaration, hoisting, scope
- [x] `let`: block scope and updating values
- [x] `const`: fixed values, arrays, and objects
- [ ] Add the proof lines from [Known Gaps](#-known-gaps--improvements)
- [ ] Temporal dead zone demo
- [ ] Data types and `typeof`
- [ ] Operators and comparison (`==` vs `===`)
- [ ] Conditionals and loops
- [ ] Functions and arrow functions
- [ ] Arrays and objects in depth
- [ ] DOM manipulation: connect this JavaScript to the CSS projects

---

<div align="center">

### ⭐ If you found this helpful, consider giving the repo a star!

Made with ❤️ while learning JavaScript

</div>
