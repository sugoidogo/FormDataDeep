# FormDataDeep
A small library for getting JSON Objects from `<form>` elements, supporting nested forms.
## Usage
```js
import FormDataDeep from 'https://sugoidogo.github.io/FormDataDeep/FormDataDeep.js';
document.forms[0].onsubmit=(event)=>{
    event.preventDefault()
    const formData=new FormDataDeep(event.target)
    // your code here
}
```
`FormDataDeep` returns a JSON Object built from the values in the native `FormData` object, plus nested objects from any descendant forms.
You can also use `new FormDataDeep(form,true)` to have values like `"on"` or `"1.0"` converted to primitives (`true` and `1.0` in this case).
## Support
Support information is listed on my [GitHub Profile](https://github.com/sugoidogo)
## Advanced Usage
This is an ES6 module exposing multiple functions, which are described below.
- `removeChildren` is an array filter predicate for use on element arrays that removes any descendants of array members from the array.
- `function getFormDataDeep(form,primitives)` calls `new FormData(form)` and converts it to a JSON Object, also converting primitives if enabled, and then recurses through `[...form.querySelectorAll('form')].filter(removeChildren)`, creating the nested or "deep" form functionality.
- `class FormDataDeep` is just a wrapper around the previous function that mimics the `FormData` interface for compatibility. Takes either an `HTMLFormElement` or a JSON Object.
    - When constructed with a JSON Object, the value of `primitives` is ignored.
    - Values can be any type, not just strings
    - An additional function, `apply`, will set all form and nested form controls to their values as stored in the `FormDataDeep`.