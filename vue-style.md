## VueJS 代码风格指南  

> 本文档内容均摘录自VueJS官方文档。

### 目录

- [命名](#命名)  
   + [单例组件名](#单例组件)  
   + [基础组件名](#基础组件)  
   + [单文件组件文件名](#单文件组件文件名)  
   + [模板中的组件名](#模板中的组件名)  
   + [JS/JSX中的组件名](#JS/JSX中的组件名)  
 
- [prop](#prop)  
- [attribute](#attribute)  


### prop

- `prop` 定义应该尽量详细。  

  > 在你提交的代码中，`prop` 的定义应该尽量详细，至少需要指定其类型。  
  
  ```javascript

   // bad
   // 这样做只有开发原型系统时可以接受
   props: ['status']

   // good
   props: {
     status: String
   }

   // best
   props: {
     status: {
       type: String,
       required: true,
       validator: function (value) {
         return [
           'syncing',
           'synced',
           'version-conflict',
           'error'
         ].indexOf(value) !== -1
       }
     }
   }
   
  ```

### attribute

- 多个 `attribute` 的元素应该分多行撰写，每个 `attribute` 一行。  

  ```javascript
  
  // bad
  <img class="classname" id="imgId" src="https://vuejs.org/images/logo.png" alt="Vue Logo">
  
  // good
  <img 
    class="classname" 
    id="imgId"
    src="https://vuejs.org/images/logo.png"
    alt="Vue Logo"
  >
  
  ```

- 元素 (包括组件) 的 attribute 应该有统一的顺序。

  > 这是我们为组件选项推荐的默认顺序。它们被划分为几大类，所以你也能知道新添加的自定义 attribute 和指令应该放到哪里。
  
  1. 定义 (提供组件的选项)  

     * `is`   
     
  2. 列表渲染 (创建多个变化的相同元素)  

     * `v-for`  
     
  3. 条件渲染 (元素是否渲染/显示)  

     * `v-if`  
     * `v-else-if`  
     * `v-else`  
     * `v-show`  
     * `v-cloak`  
     
  4. 渲染方式 (改变元素的渲染方式)  

     * `v-pre`  
     * `v-once`  
     
  5. 全局感知 (需要超越组件的知识)  

     * `id`  
     
  6. 唯一的 attribute (需要唯一值的 attribute)  

     * `ref`  
     * `key`  
     
  7. 双向绑定 (把绑定和事件结合起来)  

     * `v-model`  
     
  8. 其它 attribute (所有普通的绑定或未绑定的 attribute)  
     
  9. 事件 (组件事件监听器)  

     * `v-on`  
     
  10. 内容 (覆写元素的内容)  

      * `v-html`  
      * `v-text`  


- 为 v-for 设置键值。

  > 在组件上总是必须用 key 配合 v-for，以便维护内部组件及其子树的状态。甚至在元素上维护可预测的行为，比如动画中的对象固化 (object constancy)，也是一种好的做法。
  
  ```javascript
  
  //bad
  <ul>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ul>
  
  // good
  <ul>
    <li
      v-for="todo in todos"
      :key="todo.id"
    >
      {{ todo.text }}
    </li>
  </ul>
  ```
  
- 避免 v-if 和 v-for 用在一起，永远不要把 v-if 和 v-for 同时用在同一个元素上。

  > 一般我们在两种常见的情况下会倾向于这样做：
  
   * 为了过滤一个列表中的项目 (比如 v-for="user in users" v-if="user.isActive")。在这种情形下，请将 users 替换为一个计算属性 (比如 activeUsers)，让其返回过滤后的列表。
   
   * 为了避免渲染本应该被隐藏的列表 (比如 v-for="user in users" v-if="shouldShowUsers")。这种情形下，请将 v-if 移动至容器元素上 (比如 ul、ol)。
 
  ```javascript
  // bad
  <ul>
    <li
      v-for="user in users"
      v-if="user.isActive"
      :key="user.id"
    >
      {{ user.name }}
    </li>
  </ul>
  
  <ul>
    <li
      v-for="user in users"
      v-if="shouldShowUsers"
      :key="user.id"
    >
      {{ user.name }}
    </li>
  </ul>
  
  // good
  <ul>
    <li
      v-for="user in activeUsers"
      :key="user.id"
    >
      {{ user.name }}
    </li>
  </ul>
  
  <ul v-if="shouldShowUsers">
    <li
      v-for="user in users"
      :key="user.id"
    >
      {{ user.name }}
    </li>
  </ul>
  
  ```


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
    // 单文件组件
    <template>
      <myComponent></myComponent>
      <hiscomponent></hiscomponent>
    </template>
    
    // 字符串模板
    new Vue({
      template: '<div><myComponent></myComponent><hiscomponent></hiscomponent></div>'
    })
    
    // DOM模板
    <html>
      <body>
        <div id="templateId">
          <MyComponent></MyComponent>
          <yourComponent></yourComponent>
          <hiscomponent></hiscomponent>
        </div>
        <script>
          new Vue({
            el: '#template'
          });
        </script>
      </body>
    </html>
    
    // good
    // 单文件组件
    <template>
      <MyComponent></MyComponent>
      <his-component></his-component>
    </template>
    
    // 字符串模板
    new Vue({
      template: '<div><MyComponent></MyComponent><his-component></his-component></div>'
    })
    
    // DOM模板
    <html>
      <body>
        <div id="templateId">
          <my-component></my-component>
        </div>
        <script>
          new Vue({
            el: '#template'
          });
        </script>
      </body>
    </html>
  ```

- `JS/JSX` 中的组件名应该始终是 `PascalCase` 的。  
  
  > `JS/JSX` 中的组件名应该始终是 `PascalCase` 的，仅在使用 `Vue.component` 进行全局组件注册时，采用 `kebab-case` 风格命名组件。
  
  ```javascript
  
  // bad
  import myComponent from './MyComponent.vue'
  
  export default {
    name: 'myComponent',
    // ...
  }
  
  export default {
    name: 'my-component',
    // ...
  }
  
  Vue.component('myComponent', {
    // ...
  })
  
  // good
  import MyComponent from './MyComponent.vue'
  
  export default {
    name: 'MyComponent',
    // ...
  }
  
  Vue.component('my-component', {
    // ...
  })


## 组件/实例的选项的顺序

- 组件/实例的选项应该有统一的顺序。

  > 这是我们推荐的组件选项默认顺序。它们被划分为几大类，所以你也能知道从插件里添加的新 property 应该放到哪里。
  
1. 副作用 (触发组件外的影响)  
  
   - `el`  
     
2. 全局感知 (要求组件以外的知识)  
     
   - `name`  
   - `parent`  
  
3. 组件类型 (更改组件的类型)  
   
   * `functional`  
   
4. 模板修改器 (改变模板的编译方式)  
   
   * `delimiters`
   * `comments`  
   
5. 模板依赖 (模板内使用的资源)  
   
   * `components`  
   * `directives`  
   * `filters`  
   
6. 组合 (向选项里合并 property)  
   
   * `extends`  
   * `mixins`  

7. 接口 (组件的接口)  
   
   * `inheritAttrs`  
   * `model`  
   * `props/propsData`  
   
8. 本地状态 (本地的响应式 property)  
   
   * `data` 
   * `computed`  

9. 事件 (通过响应式事件触发的回调)  
   
   * `watch`  
   * `生命周期钩子 (按照它们被调用的顺序)`  
   
      + beforeCreate  
      + created  
      + beforeMount  
      + mounted  
      + beforeUpdate  
      + updated  
      + activated  
      + deactivated  
      + beforeDestroyed  
      + destroyed  

10. 非响应式的 property (不依赖响应系统的实例 property)  
   
    * `methods`  

11. 渲染 (组件输出的声明式描述)  
   
    * `template/render`  
    * `renderError`  



   
## 单文件组件的顶级元素的顺序。  

  > 单文件组件应该总是让 <script>、<template> 和 <style> 标签的顺序保持一致。且 <style> 要放在最后，因为另外两个标签至少要有一个。  
  
  ```javascript
  
  // bad
  
  <style>/* ... */</style>
  <script>/* ... */</script>
  <template>...</template>
  
  <!-- ComponentA.vue -->
  <script>/* ... */</script>
  <template>...</template>
  <style>/* ... */</style>
  
  <!-- ComponentB.vue -->
  <template>...</template>
  <script>/* ... */</script>
  <style>/* ... */</style>
  
  // good
  
  <!-- ComponentA.vue -->
  <script>/* ... */</script>
  <template>...</template>
  <style>/* ... */</style>

  <!-- ComponentB.vue -->
  <script>/* ... */</script>
  <template>...</template>
  <style>/* ... */</style>
  
  <!-- ComponentA.vue -->
  <template>...</template>
  <script>/* ... */</script>
  <style>/* ... */</style>

  <!-- ComponentB.vue -->
  <template>...</template>
  <script>/* ... */</script>
  <style>/* ... */</style>
  
  ```
