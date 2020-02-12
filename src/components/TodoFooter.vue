<template>
    <div class="clearAllContainer">
        <button type="button" class="clearAllBtn" v-on:click="clearTodo">Clear All</button>
    </div>
</template>

<script>
export default {
    methods: {
        clearTodo : function() {
            this.$emit('clearAll');
        }
    }
}
</script>

<style scoped>
    .clearAllContainer {
        width: 8.5rem;
        height: 50px;
        line-height: 50px;
        background-color: white;
        border-radius: 5px;
        margin: 0 auto
    }
    .clearAllBtn {
        border: none;
        line-height: 50px;
        margin-top:20px;
        text-align: center;
        width:100%;
        color: #e20303;
        display: block;
    }
</style>