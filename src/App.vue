<template>
  <div id="app">
    <todo-header></todo-header>  
    <todo-input v-on:addTodoItem="addOneItem"></todo-input> 
    <todo-list v-bind:propsdata="todoItems" 
      v-on:removeItem="removeOneItem" 
      v-on:toggleItem="toggleOneItem"></todo-list>
    <todo-footer v-on:clearAll="clearAllItem"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data: function() {
    return {
      todoItems: []
    }
  },
  methods: {
    addOneItem: function(todoItem) {
      var obj = {completed: false, item: todoItem};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);
    },
    removeOneItem: function(todoItem, index) {
      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);
    },
    toggleOneItem: function(todoItem, index) {
      this.todoItems[index].completed = !this.todoItems[index].completed;
            
      // 로컬 스토리지 데이터를 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItem: function() {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created: function() {
      if (localStorage.length > 0) {
          for (var i = 0; i < localStorage.length; i++) {
              if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
                  this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                  // this.todoItems.push(localStorage.key(i));
              }
          }
      }
  },
  components: {
    // '컴포넌트 태그명': 컴포넌트 내용
    'todo-header': TodoHeader,
    'todo-input': TodoInput,
    'todo-list': TodoList,
    'todo-footer': TodoFooter,
  }
}
</script>

<style>
  html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, s, samp, small, strike, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary, time, mark, audio, video {margin:0;padding:0;border:0;font:inherit}
  article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section {display:block}
  body {line-height:1;-webkit-text-size-adjust:none;font-size:14px}
  ol, ul {list-style:none}
  blockquote, q {quotes:none}
  blockquote:before, blockquote:after,
  q:before, q:after {content:none}
  table {border-collapse:collapse;border-spacing:0;table-layout:fixed}
  hr {display:none}
  img {vertical-align:top}
  em, i, address {font-style:normal}
  a {text-decoration:none}
  legend, caption {position:absolute;width:1px;height:1px;clip:rect(1px, 1px, 1px, 1px)}
  /* form element */
  input,
  textarea,
  button,
  select {-webkit-appearance:none;padding:0;border-radius:0;font-size:14px}
  input[type="checkbox"],
  input[type="radio"] {margin:0; border:1px solid #999}
  input[type="radio"] {-webkit-appearance:radio}
  input[type="checkbox"] {width:20px;height:20px;border:1px solid #909191;-webkit-appearance:checkbox}
  input:checked[type="checkbox"],
  input:checked[type="radio"] {background-color:#2d2d2d}
  input::-webkit-input-placeholder {color:#999}
  input[type="number"],
  input[type="tel"],
  input[type="text"],
  input[type="password"],
  input[type="email"],
  input[type="search"],
  textarea {border:1px solid #ccc}
  input[type="search"]::-webkit-search-decoration,
  input[type="search"]::-webkit-search-cancel-button,
  input[type="search"]::-webkit-search-results-button,
  input[type="search"]::-webkit-search-results-decoration {display:none}
  button{cursor:pointer;border:none;background:none;box-sizing:border-box;}

  .blind {position:absolute;width:1px;height:1px;clip:rect(1px,1px,1px,1px)}
  body {
    text-align:center;
    background-color:#f6f6f6;
  }
  input {
    border-style:groove;
    width:200px;
  }
  button {
    border-style:groove;
  }
  .shoadow {
    box-shadow:5px 5px 5px rgba(0, 0, 0, .1)
  }
</style>