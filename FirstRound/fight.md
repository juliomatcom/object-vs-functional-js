### First round :collision:
- OOP  
  ```javascript

  function Cat (sound) {
    this.sound = sound;
    this.speak = function () {// impure function
      console.log(this.sound);
    }
  }
  let cat = new Cat('miau');

  let el = document.getElementById('catButton');
  el.addEventListener('click', cat.speak);

  el.click(); // undefined
  ```
  :facepunch: :dizzy_face:
  What, Why ?  <span style="float: right;"> <a href="https://jsfiddle.net/juliomatcom/pmn39nnn/">open in jsfiddle</a></span>  

  As [Mozilla MDN](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) explain:
  >  When attaching a **handler function** to an element using `addEventListener()`, the **value** of `this` inside the handler is a **reference to the element**.

  The function `cat.speak` will be called in the context of `el` and `this.sound` will be `undefined` :(  

- FP  
  Lets see the functional approach
  ```javascript
  let logValueFun = function (value) {// pure function
    return function () {
      console.log(value);
    }
  }
  let catSpeak = logValueFun('miau');

  let el = document.getElementById('catButton');
  el.addEventListener('click', catSpeak);

  el.click(); // miau
  ```
  :thumbsup:  See ? <span style="float: right;"> <a href="https://jsfiddle.net/juliomatcom/jewun21y/">open in jsfiddle</a></span>  

  All we do is pass a pure function that **not depends** on the context around, the result of a pure function will never depends on the `this` state. Pure functions are more **expressive and declarative**, all its dependencies will be passed as arguments always.
