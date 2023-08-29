# Using ChatGPT in this class


## I. Here's an allowable use of ChatGPT in this course - as a research tool
- [ChatGPT 3.5 - How do I make an HTTP request in Javascript?](https://chat.openai.com/c/5093bcc2-39ec-455e-a611-647ef44741f8)
- Clicking on the link above should give you a "live" answer (assuming you have a free account) - below is a capture from a few days ago

![screenshot](_images/chat-gpt-1.png)

![screenshot](_images/chat-gpt-2.png)

![screenshot](_images/chat-gpt-3.png)

![screenshot](_images/chat-gpt-4.png)

<hr>

## II. So now you've got some code!

- **Four** distinct solutions are given ...
- Some might just copy/paste the first answer? (A common and unfortunate Stackoverflow.com "workflow" ...)
  - but as stated in the syllabus - *"If I doubt authorship, I may ask you to explain the code or re-create aspects of the code"*
- Questions you might have about this code:
  - What is the difference between a `GET` and a `POST` Request? Which should I use?
  - Should I use `XHR` or `fetch()`? What are the advantages and disadvanatges of each?
  - The first code block sets a *request header* - what's that? Is it necessary to set those?
  - What are the `readyState` and `status` properties? What are the possible values?
  - This code block uses `var` (not allowed in this course) and the `function` keyword instead of the arrow functions seen in the later code examples. Does this mean that `XHR` only works with `var` and `function`?
  - What does `JSON.stringify()` do?
  - What are `.then()` and `.catch()` and *Promises*?
  - Why are there 2 `.then()` methods chained together?
  - `XHR` is supported in older browsers, does that mean it's NOT supported in newer browsers?

<hr>

## III. Discussion

- Before you utilize ("hand in") any of the code from above, you should be able to answer most of the above questions \
- You will undoubtedly need to re-factor some of this code:
  - `let` and `const` instead of `var`
  - named arrow functions where possible to aid in debugging
  - get rid of unnecessary code (ex. don't always need to send headers)
  - add error handling
- 


