## 组件命名

-  `单文件组件` 的 `文件名` 应该是 `PascalCase` 风格。
  
  > `kebab-case` 风格也可取，但是出于一致性考虑，尽量使用 `PascalCase` 风格
  
  ```javascript
  
    // bad 
    components/
    |- mycomponent.vue
    
    components/
    |- myComponent.vue
    
    // good 
    components/
    |- my-component.vue
    
    // best
    components/
    |- MyComponent.vue
  ```


- `Vue.component` 进行全局组件注册时，使用 `kebab-case` 命名。
  
  ```javascript
  
    // bad 
    Vue.component('myComponent', {
      // ...
    })
    
    // good 
    Vue.component('MyComponent', {
      // ...
    })
    
    // best
    Vue.component('my-component', {
      // ...
    })
  ```
  
- 模板中的组件名大小写。
  
  > 在 `单文件组件` 和 `字符串模板` 中使用组件时组件名应该总是 `PascalCase` 风格的——但是在 `DOM 模板` 中使用组件时组件应该是 `kebab-case` 风格的。
  
    ```javascript
  
    // bad 
    
    // 单文件组件中
    <template>
      <myComponent></myComponent>
    </template>
    
    // 字符串模板
    new Vue({
      template: '<myComponent></myComponent>'
    })
    
    // DOM模板
    Vue.component('myComponent', {
      // ...
    })
    
    // good 
    Vue.component('MyComponent', {
      // ...
    })
    
    // best
    Vue.component('my-component', {
      // ...
    })
  ```

- `JS/JSX` 中的组件名应该始终是 `PascalCase` 的。  


- 在单文件组件和字符串模板中组件名应该总是 PascalCase 的——但是在 DOM 模板中总是 kebab-case 的。

-
