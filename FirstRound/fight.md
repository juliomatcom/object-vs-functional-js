### First round :collision:
- OOP  
  ```javascript

  function Cat (sound) {
    this.sound = sound;
    this.speak = function () {// impure
      console.log(this.sound);
    }
  }
  let cat = new Cat('miau');

  let catSound = cat.speak;
  catSound(); // undefined

  catSound.apply(cat); // miau
  ```

  How ?   
In javascript the function context is the object who call the function, because in this case `catSound` is attached to the context of the function because of the `this` we can not call `catSound` without bind a context.

- FP  
  ```javascript
  let logValueFun = function (value) {// pure function
    return function () {
      console.log(value);
    }
  }

  function makeCats (state) {
    return Object.assign({}, state, {
      speak: logValueFun(state.sound)
    })
  }

  let cat = makeCats({
    sound: 'miau'
  });
  let catSound = cat.speak;

  catSound(); // miau
  ```  
  *Hit down!* Now this is possible because `catSound` is a pure function that not depends on the environment that sorrounds it, in this case the intance of cat
