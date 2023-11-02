# HW-3 - Web App refactor (DRAFT)

---

## Overview
- For this HW you will choose a web app you previously created in IGME-235 or IGME-330, and will update the UI and refactor the code

---

## I. Choose a web app to refactor
- There are two "pre-approved" web apps you may use:
  - IGME-330's [HW-2 - Audio Visualizer - Ultimate Version](../hw/hw-2.md)
  - IGME-235's [Project 2 - Web Service Application](https://github.com/dccircuit/IGME-235-Fall-2023/blob/main/projects/project-2.md)
- ***If there is a different project you would rather refactor, ask (well) in advance of the due date***
- Put everything in a folder named ***coder-a*-hw-3-refactor** (with ***coder-a*** replaced by your actual last name and initial)
  
--- 

## II. Refactor the app's HTML
- The app's HTML file shall be named **index.html**
- Make sure that the HTML inside **index.html** follows our course naming standards ("kebab-case" for `id` and `class` names, etc)
- The HTML must pass the validator at: https://validator.w3.org/
- All files (.html, .js, .css etc) must follow course naming standards (kebab-case, no spaces etc)
- ***If you are refactoring HW-2 - Audio Visualizer, this will not take too long***
---

## III. Refactor the JS
- all regular functions (including anonymous functions) will be refactored to utilize `const` and arrow function syntax
- variable and function names must follow course naming standards
- all code will be located in ES6 module files that use `import` and/or `export` as we have been doing all semester
  - if needed, refactor the code to "separate concern" into specific logical modules (meaning, separate .js files that utilize `export` and/or `import`)
  - ES6 `class` declarations ***MUST*** be in their own distinct file (ex. **CircleSprite.js** or **RectangleSprite.js** etc...)
- ***If you are refactoring HW-2 - Audio Visualizer, this will not take too long***
  
---

## IV. Refactor the CSS with Bulma
- use [PE-08 - Bulma I - Intro to Bulma](../pe/pe-08.md) as a "starter" page
- reimplement the app UI in the starter page
- use appropriate Bulma classes (for buttons etc)
- ...

---

## V. Add an about.html page

---

## VI. Choose a language to code in (15%)

- **Option #1** - ES6 "Vanilla" JavaScript (max grade for this section is 0%)
  - just do what we've been doing all semester (ES6 modules, arrow functions, `let` & `const` etc)
- **Option #2** - TypeScript (max grade for this section is 15%)
  - Review:
    - [Intro to TypeScript](https://github.com/tonethar/IGME-330-Master/blob/master/notes/intro-typescript.md)
    - [Checkoff - TypeScript Practice](../checkoffs/typescript-practice.md)
    - Make substantial use of TypeScript in your code: interfaces, enums and strongly typed variables, function parameters, and function return types
- **Option #3** - React (max grade for this section is 15%)

---

## VII. Bundle the code (15%)
- For **option #1** (ES6 Vanilla JS) above, be sure to transpile the code to ES5 and bundle it per these instructions: [Bundling & Transpiling JS](../notes/bundling-transpiling.md)
- For **option #2** (TypeScript) above, be sure to transpile the code to ES5 and bundle it per these instructions: [Intro to TypeScript](https://github.com/tonethar/IGME-330-Master/blob/master/notes/intro-typescript.md)
- For **option #3** (React) above
  
---

## VIII. Documentation
- Tell us what language you coded in
- For options #2 & #3, describe the code changes you implemented

---

## IX. Submission
- ZIP and Post to myCourses
  - Your completed ***coder-a*-hw-3-refactor** folder (with **node_modules** deleted)
  - The original version of the web app you re-factored:
    - if you refactored *HW-2 - Audio Visualizer - Ultimate Version*, I already have that, so don't worry about re-submitting it
- Post the completed HW-3 to banjo
- Required Documentation


