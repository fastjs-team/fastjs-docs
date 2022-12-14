# Element

:::tip Authoritative document
This page is for senior users. If you are a junior user, you can skip this page.
:::

## Create Element List

### Prototype

```typescript
class fastjsDomList {
    constructor(list: Array<HTMLElement> = []) {}
}
```

### Example

FastjsDomList receives `Array<HTMLElement>`

```javascript
import { FastjsDom } from 'fastjs-next';

const element = new FastjsDomList();
```

```javascript
import { FastjsDom } from 'fastjs-next';

const element = document.createElement("div");
const fastjsDomList = new FastjsDomList([element]);
```

## Set index

### Prototype

```typescript
class fastjsDomList {
    html<T extends string>(val: T): T extends undefined ? string : fastjsDomList {}
    text<T extends string>(val: T): T extends undefined ? string : fastjsDomList {}
}
```

### Example

Use `html` or `text` to set the index of the element.

```javascript
import { selector as $ } from 'fastjs-next';

$("div").text("I am div");
```

### Difference between html and text

```text
el.html(text) -> each -> el.innerHTML = text -> el
el.text(text) -> each -> el.innerText = text -> el
```

## Get index

### Example

Use `html` or `text` to get the index of the fastjsDomList[0].

```javascript
import { selector as $ } from 'fastjs-next';

$("body").html("<span>1</span><span>2</span><span>3</span>");
console.log($("span").text()); // 1
```

## Set value <Badge text="v1.2.1" type="tip"/>

:::warning
After v1.2.0, val become stricter. Parameter `val` only be `string | undefined`.
:::

### Prototype

```typescript
class fastjsDom {
    val(): string
    val(val: string): FastjsDomList
    
    val(val?: string): FastjsDomList | string {}
}
```

### Example

Use `val` to set or get the value of the `input`, `textarea` and `button` element.

```javascript
import { selector as $ } from 'fastjs-next';

$("input").val("Hello World");
console.log($("input").val()); // Hello World
```


## Set attribute

### Prototype

```typescript
class fastjsDomList {
    attr(key: string): string | null
    attr(key: string, value: string | null): fastjsDomList

    attr(key: string, value?: string | null): string | null | fastjsDomList {}
}
```

### Example

Use `attr` to set the attribute of the element.

```javascript
import { selector as $ } from 'fastjs-next';

$("div").attr("i-am", "div");
```

## Style

### v1.1.0

### Prototype

```typescript
class fastjsDomList {
    css(): CSSStyleDeclaration
    css(key: object): fastjsDomList
    css(key: string, value: string, other?: string): fastjsDomList

    css(key?: string | object, value?: string, other?: string): fastjsDomList | CSSStyleDeclaration {}
}
```

### Example

Use `css` to set the style of the element.

```javascript
import { selector as $ } from 'fastjs-next';

$("span").css("color", "red");
```

This style is important? Write like this

```javascript
import { selector as $ } from 'fastjs-next';

$("span").css("color", "red", true);
```

You can also use object to set the style of the element.

```javascript
import { selector as $ } from 'fastjs-next';

$("span").css({
    "color": "red",
    "font-size": "20px"
});
```

### v1.0.14 <Badge text="obsolete" type="warning"/>

### Example

Use `css` to set the style of the element.

```javascript
import { selector as $ } from 'fastjs-next';

$("span").css("color", "red !important");
```

## Event <Badge text="v1.1.0" type="warning"/>

### Prototype

```typescript
class fastjsDomList {
    on(event: string = "click", callback: Function): fastjsDomList {}
    off(event: string = "click", callback: Function): fastjsDomList {}
}
```

Callback function:

```typescript
function callback(el: FastjsDom, ...EventListenerCallback): void {}
```

### Example

### on

Use `on` to add event to the element.

```javascript
import { selector as $ } from 'fastjs-next';

$("body").on("click", (el) => {
    console.log(el, "clicked");
});
```

### off <Badge text="v1.1.0" type="tip"/>

Use `off` to remove event from the element.

```javascript
import { selector as $ } from 'fastjs-next';

const callback = (el) => {
    console.log(el, "clicked");
    el.off("click", callback);
};
$("body").on("click", callback);
```

## Change to Element

### Prototype

```typescript
class fastjsDomList {
    el(key): HTMLElement {}
    getEl(key): fastjsDom {}
}
```

### Example

Use `el(key)` to change FastjsDomList -> FastjsDom to Element.

```javascript
import { selector as $ } from 'fastjs-next';

console.log($("div").el()); // Element
```

Use `getEl(key)` to get FastjsDom in FastjsDomList.

```javascript
import { selector as $ } from 'fastjs-next';

console.log($("div").getEl()); // FastjsDom
```

## Access element <Badge text="v1.1.2" type="tips"/>

:::tip
You can also use `el()` to get the element.
:::

### Prototype

```typescript
class fastjsDom {
    set<T extends keyof HTMLElement>(key: T, val: HTMLElement[T], el?: number): fastjsDom {}
}
```

Use `set(index, value, set)` to operate element.

```javascript
import { selector as $ } from 'fastjs-next';

$("body > *")
  .set("innerHTML", "<span>Hello World</span>")
  .set("innerHTML", "<h1>Title</h1>", 0)
```

## Get Parent

### Prototype

```typescript
class fastjsDomList {
    father(): fastjsDom {}
}
```

### Example

Use `father()` to get the parent of the fastjsDomList[0].

```javascript
import { selector as $ } from 'fastjs-next';

$("body").html("<div></div>");
console.log($("div").father()); // FastjsDom -> body
```

## ForEach <Badge text="v1.1.2" type="tips"/>

:::tip eachCallback -> index
Query `index` is available after v1.2.1.
:::

### Prototype

```typescript
type eachCallback = (el: FastjsDom, dom: HTMLElement, index: number) => void;

class fastjsDomList {
    each(callback: eachCallback): fastjsDomList {}
}
```

### Example

Use `each` to loop the FastjsDomList.

```javascript
import { selector as $ } from 'fastjs-next';

$("body > *").each((el, dom, index) => {
    console.log(el, dom, index);
});
```

## Manage FastjsDomList

### Prototype

```typescript
class fastjsDomList {
    add(el: FastjsDom | HTMLElement): FastjsDomList {}
    delete(key: number, deleteDom: boolean = false): FastjsDomList {}
}
```

### Example

Use `add` to add FastjsDom to FastjsDomList.

```javascript
import { selector as $ } from 'fastjs-next';

const list = new FastjsDomList();
list.add($("div").getEl());

// or
$("div").each(list.add)
```

Use `delete` to delete FastjsDom from FastjsDomList.

```javascript
import { selector as $ } from 'fastjs-next';

$("div").delete(0); // fastjsDomList without the first div

// or
$("div").delete(0, true); // fastjsDomList without the first div and remove it from the DOM
```

## Length

### Prototype

```typescript
class fastjsDomList {
    length: number
}
```

### Example

Use `length` to get the length of FastjsDomList.

```html
<div></div>
<div></div>
<div></div>
<div></div>
```

```javascript
import { selector as $ } from 'fastjs-next';

console.log($("div").length); // 4
```