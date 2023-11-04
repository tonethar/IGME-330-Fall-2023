# Converting an existing project to TypeScript

---

## I. Get ready!
- Before you start writing your TypeScript, run your app in Liveserver to be 100% sure that it works!

---

## II. Set up the TypeScript/Webpack tooling
***With the app you want to refactor***:

- Follow the instructions here: [Intro to TypeScript#Use node & webpack to transpile a TypeScript app to JS](https://github.com/tonethar/IGME-330-Master/blob/master/notes/intro-typescript.md#iii-use-node--webpack-to-transpile-a-typescript-app-to-js)
- Don't forget to edit your HTML file to use the transpiled code in the **dist/** folder:
  - comment out the `<script>` tag in the `<head>` of the document
  - and then add `<script src="./dist/bundle.js"></script>` to the bottom of the page
- In **webpack.config.js** `entry:` change the filename from **main.ts** to whatever the "entry point" file of your app is
- Type: `npm run build`
  - ERRORS!
    - ***ERROR TS18003: No inputs were found in config file 'tsconfig.json'. Specified 'include' paths were '["src/**/*"]' and 'exclude' paths were '[]'***
    - ***error while parsing tsconfig.json***
  - you may have previously noticed an error in **tsconfig.json** - basically, `npm` and `typescript` are complaining because they can't find any Typescript **.ts** files
- Pathetically, there is a very simple solution:
    - in **src/** create and save a file named **empty.ts**
    - `npm run build` again - and compilation will succeed?
       - yes, kind of - but because **dist/bundle.js** is actually empty - we did not accomplish much
       - delete **empty.ts**
- Instead, go ahead and change the file extension on all of your **.js** files to **.ts**
  - also, change the file extensions of all of your imports from **.js** to **.ts**
    - example `import * as audio from './audio.js';` becomes `import * as audio from './audio.ts'`
  - in **webpack.config.js** `entry:` change the file extension of then entry point to **.ts**
    - NB: whenever you change a "config" file, always be sure to type `ctrl-c` to quit `webpack` and then restart it so that the config changes are loaded
  - quit `webpack` and then `npm run build` again:
    - probably a bunch of errors - mostly legitimate TypeScript issues you need to fix
    - but there's one more error message we FIRST need to get rid of:
      - ***TS5097: An import path can only end with a '.ts' extension when 'allowImportingTsExtensions' is enabled.***
- To solve this error, we could edit the config files, but instead we'll use the "safest" and most backwardly compatible way to fix the error, which is to get rid of the file extensions from your `import` statements - example:
  
```js
// CHANGE THIS (in main.ts):
import * as audio from './audio.ts';
import * as utils from './utils.ts';
import * as canvas from './canvas.ts';

// TO THIS:
import * as audio from './audio';
import * as utils from './utils';
import * as canvas from './canvas';

// DO THIS IN ALL OF YOUR JS FILES THAT HAVE IMPORTS
````

- Quit `webpack` and then `npm run build` again
- You will likely have just a bunch of typescript errors at this point (which is good!)
- And now you can finally get to work on fixing the code instead of fighting the tooling!
  
---

## III. Fix TypeScript errors

- You should see a long list of errors in the console, but it's probably easier to handle them one file at a time
- In VS Code any file with errors should be highlighted in red, and show the number of errors 

---

### III-A. Fixing errors in canvas.ts
- My **canvas.ts** (from the Audio Visualizer PE) has 6 errors - so I'll start with those
- Note: TypeScript is also giving a lot of "hints" (not errors) with dashed gray underlines:
  - for example *Variable 'ctx' implicitly has an 'any' type, but a better type may be inferred from usage.ts(7043)*
  - I am going to IGNORE these hints for now and will come back to them only AFTER I have eliminated all of the errors in ALL of the code files, and have also confirmed that the app is bundled up and running as expected in  a web browser
- Here's my first error - kind of a tricky one:
  - ***Property 'showGradient' does not exist on type '{}'.ts(2339)***

```js
// 3 - draw gradient
if(params.showGradient){ ...
````

- And the error is repeated multiple times in the file:

```js
if(params.showBars){ ...
if(params.showCircles){ ...
etc ...
```

- To fix these errors, I need to declare a TypeScript `interface` at the top of **canvas.ts**
  - https://www.typescriptlang.org/docs/handbook/interfaces.html
    
```ts
interface DrawParams{
  showGradient: boolean,
  showBars?: boolean,
  showCircles?: boolean,
  // etc ...
}
```

- To use the `DrawParams` interface, change the start of `draw()` to look like this:
  - `const draw = (params:DrawParams) => {...`
- After adding in the other possible (optional) values for draw params, that knocked off all 6 of my **canvas.ts** errors

---

### III-B. Fixing errors in main.ts

- Next up: - my **main.ts** (from the Audio Visualizer PE) has 22 errors
- Here's the first error:
  - ***Property 'onclick' does not exist on type 'Element'.ts(2339)***
  
```ts
fsButton.onclick = e => { ...
```

- Which just simply means that Typescript doe not know that `fsButton` is an HTML element
  - this is easily fixed by using a **type assertion** - `as`:

```ts
// CHANGE THIS
const volumeSlider = document.querySelector("#volumeSlider");

// TO THIS
const volumeSlider = document.querySelector("#volumeSlider") as HTMLInputElement;
```

- Next error up:
  - ***Property 'value' does not exist on type 'EventTarget'.ts(2339)***

```ts
volumeSlider.oninput = e => {
  //set the gain
  audio.setVolume(e.target.value); // Typescript does not know what type e.target is
  ...
```

- You could fix this by making a temp variable named `target`, and then reusing it in this event handler function:

```ts
 volumeSlider.oninput = e => {
    const target = e.target as HTMLInputElement;
    //set the gain
    audio.setVolume(target.value);
    ...
```

- You might also see ***Type 'number' is not assignable to type 'string'.*** error
  - this means that a property is expecting a string type as a value, not a number
  - to fix this, convert the value to a string
- Another error was ***The left-hand side of an arithmetic operation must be of type 'any', 'number', 'bigint' or an enum type***
  - in this case, it meant that the left-hand side value was a string, when it should have been a number
  - to fix this, convert the value to a number
  - hint: the `value` property of HTML `<input>` tags is ALWAYS a string - which means that sometimes you have to cast it to a number before you can use it
- After much use of **type assertions**, all of the errors are gone
  
---

### III-C. Fixing errors in audio.ts
- Just one error in **audio.ts**
  - if you see ***Property 'webkitAudioContext' does not exist on type 'Window & typeof globalThis'. Did you mean 'AudioContext'?ts(2551)***

```ts
CHANGE THIS:
const AudioContext = window.AudioContext || window.webkitAudioContext;

TO THIS:
const AudioContext = window.AudioContext;

// we really don't need the `webkitAudioContext` stuff anymore
// https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API/Migrating_from_webkitAudioContext
```

- Once all of the TypeScript errors are gone from all of your **.ts** files, move on
  
---

## IV. Test the converted app in the browser
- Now that all of the TypeScript errors are gone, it's time to test the app in a browser
- Check **dist/bundle.js** to be sure that there is ES5 code in it now
- As mentioned at the beginning, don't forget to edit your HTML file to use the transpiled code in the **dist/** folder:
  - comment out the `<script>` tag in the `<head>` of the document
  - and then add `<script src="./dist/bundle.js"></script>` to the bottom of the page
- Launch Live Server (you need a web server because of Web Audio and Canvas imageData access) and test the app in a browser!
- Assuming everything works perfectly, move on ...

---

## V. Keep re-factoring the code
- Now that you've dealt with TypeScript errors, it's time to deal with the TypeScript "hints" - which are underlined with dashed gray lines
- **audio.ts**
  - Go ahead and *strongly type*:
    - `let audioCtx;` to `let audioCtx:AudioContext;`
    - `let element` to `let element:HTMLAudioElement`
    - etc
  - Turn `const DEFAULTS` into a "real" TypeScript `enum`
    - https://www.typescriptlang.org/docs/handbook/enums.html
    - Then put it in **src/enums/audio-defaults.enum.ts** and `export`/`import` it
  - Note that `let audioData = new Uint8Array(DEFAULTS.numSamples/2);` is unused
    - you can delete it
  - Strongly type your function parameters
- **canvas.ts**
  - Put the `DrawParams` interface in a external file named **src/types/drawParams.interface.ts** and `export`/`import` it where needed
  - Strongly type your variables where needed:
    - `let ctx` becomes `let ctx:CanvasRenderingContext2D`
    - etc
  - Strongly type your function parameters
- **main.ts**
  - `import` your `DrawParams` interface and strongly type the local `drawParams` object
  - Strongly type your variables where needed:
  - Strongly type your function parameters
- **utils.ts**
  - Strongly type your function parameters
    - `colorStops` is the only one that will be tricky - it needs an interface
    - Hint: create a `interface ColorStop{...}`  first
   
---
---
