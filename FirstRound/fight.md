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
  Because in javascript the function context is who called her, so in this case `catSound` is not called from any object.

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
