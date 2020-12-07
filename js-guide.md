# Javascript编码规范

[1 空白](#1-空白)

[1.1 空格](#11-空格)

[1.2 空行](#12-空行)

## 1 空白

### 1.1 空格

- 将软tab设置为两个空格。

    ```javascript
    // bad
    function foo() {
    ∙∙∙∙const name;
    }

    // bad
    function bar() {
    ∙const name;
    }

    // good
    function baz() {
    ∙∙const name;
    }
    ```

- 在起始花括号前加一个空格。

    ```javascript
    // bad
    function test(){
      console.log('test');
    }

    // good
    function test() {
      console.log('test');
    }

    // bad
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // good
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

- 在控制语句的圆括号前加一个空格 (if，while 等)。 在函数调用和声明中在参数列表和函数名间不要放置空格。

    ```javascript
    // bad
    if(isJedi) {
      fight ();
    }

    // good
    if (isJedi) {
      fight();
    }

    // bad
    function fight () {
      console.log ('Swooosh!');
    }

    // good
    function fight() {
      console.log('Swooosh!');
    }
    ```

- 二元运算符两边放置空格。

    ```javascript
    // bad
    const x=y+5;

    // good
    const x = y + 5;
    ```
    
- 圆括号中不要添加空格。

    ```javascript
    // bad
    function bar( foo ) {
      return foo;
    }

    // good
    function bar(foo) {
      return foo;
    }

    // bad
    if ( foo ) {
      console.log(foo);
    }

    // good
    if (foo) {
      console.log(foo);
    }
    ```

- 不要在方括号内添加空格

    ```javascript
    // bad
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // good
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

- 在花括号中添加空格。

    ```javascript
    // bad
    const foo = {a: 1}
    function foo () {return true} 

    // good
    const foo = { a: 1 }
    function foo () { return true } 
    ```

- 逗号前不要加空格，逗号后要加空格。

    ```javascript
    // bad
    var foo = 1,bar = 2
    var arr = [1 , 2]
    var bar = { a: 1,b: 2 }

    // good
    var foo = 1, bar = 2
    var arr = [1, 2]
    var bar = { a: 1, b: 2 }
    ```

- 对象字面量属性中的 : 之后必须有空格，: 之前不允许有空格。

    ```javascript
    // bad
    var obj = { a : 42 };
    var obj2 = { a:42 };

    // good
    var obj = { a: 42 };
    ```

- 行尾不得有多余的空格。

    ```javascript
    // bad
    var obj = { a: 1 }∙∙

    // good
    var obj = { a: 1 }
    ```



### 1.2 空行

- 用空行结束文件。

    ```javascript
    // bad
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;
    ```

    ```javascript
    // bad
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ↵
    ```
    
- 在代码块结束和下一个声明前留一个空行。

    ```javascript
    // bad
    if (foo) {
      return bar;
    }
    return baz;

    // good
    if (foo) {
      return bar;
    }

    return baz;

    // bad
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // good
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // bad
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // good
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

- 清除代码中的冗余空行。

    ```javascript
    // bad
    function bar() {

      console.log(foo);

    }

    // also bad
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // good
    function bar() {
      console.log(foo);
    }

    // good
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

