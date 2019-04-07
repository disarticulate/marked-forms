# marked-forms
[![Azure Build Status](https://dev.azure.com/jldec/marked-forms/_apis/build/status/jldec.marked-forms?branchName=master)](https://dev.azure.com/jldec/marked-forms/_build/latest?definitionId=1&branchName=master)
[![Build Status](https://travis-ci.org/jldec/marked-forms.svg?branch=master)](https://travis-ci.org/jldec/marked-forms)

Custom [marked renderer](https://marked.js.org/#/USING_PRO.md#renderer) to generate html form inputs.

## installation

```sh
npm install marked-forms
```

## usage

```javascript
var marked = require('marked');
var renderer = new marked.Renderer();

// note as of v2.0.0, the 2nd parameter is required to monkey-patch marked to support
// spaces in the url part of links, which is used for the form-field name attribute.

require('marked-forms')(renderer, marked);    // monkey-patches the renderer

var html = marked(markdown, {renderer:renderer});
```

## **text** input

markdown

```md
[Provide a Name ??]()
```

html

```html
<label for="provide-a-name">Provide a Name</label>
<input name="Provide a Name" id="provide-a-name">
```

- `??` at the start or end of the link text results in an `<input>` with a `<label>` before or after it.

- `id` and `for` and `name` attributes are derived from the text.

- `id` and `for` are sluglified, `name` is not.

- explicit `id`, `for`, `name` can be specified by doing

```md
[Different label ??](nme)
```

```html
<label for="nme">Different label</label>
<input name="nme" id="nme">
```

- if you don't need need any label, just do `[??](nme)`

```html
<input name="nme" id="nme">
```


## **select**

markdown

```md
[Choose one ?select?](nme)
- option1
- option2
- option3
```

html

```html
<label for="nme">Choose one</label>
<select name="nme" id="nme">
<option value="option1">option1</option>
<option value="option2">option2</option>
<option value="option3">option3</option>
</select>
```

## **check list**

markdown

```md
[?checklist?](name)
- check1
- check2
- check3
```

html

```html
<label class="checkbox">check1<input type="checkbox" name="name" value="check1"></label>
<label class="checkbox">check2<input type="checkbox" name="name" value="check2"></label>
<label class="checkbox">check3<input type="checkbox" name="name" value="check3"></label>
```

#### there's more
Additional doc coming soon. For now check out [code](marked-forms.js) and [tests](test/test-marked-forms.js).

