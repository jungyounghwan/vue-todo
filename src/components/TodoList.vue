<template>
    <div>
        <ul class="todo_list">
            <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shoadow">
                <input type="checkbox" class="checkbox" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
                    v-on:click="toggleComplete(todoItem, index)" v-bind:checked="todoItem.completed">
                <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
                <button v-on:click="removeTodo(todoItem, index)" class="remove_btn">del</button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: ['propsdata'],
    methods: {
        removeTodo: function(todoItem, index) {
            this.$emit('removeItem', todoItem, index);
        },
        toggleComplete: function(todoItem, index) {
            this.$emit('toggleItem', todoItem, index);
        }
    }
}
</script>

<style scoped>
    .todo_list {width:90%;margin:0 auto}
    .todo_list li {position:relative;background:#fff;border-radius:5px;line-height:30px;margin-top:15px;text-align:left;padding:10px;}
    .todo_list li .checkbox {vertical-align:middle;}
    .todo_list li .remove_btn {position:absolute;border:1px solid #aaa;line-height:15px;margin-top:-13px;padding:5px;right:10px;top:50%;border-radius:5px}
    .todo_list li .checkBtnCompleted {color:#b3adad}
    .todo_list li .textCompleted {text-decoration:line-through;color:#b3adad}
</style>