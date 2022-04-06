<template>
    <div class="todo-footer">
        <label>
            <input type="checkbox" :checked="allDone" @change="checkAll">
        </label>
        <span>
            <span>已完成{{doneSize}}</span> / 全部{{todoList.length}}
        </span>
        <button class="btn btn-danger" @click="clearDone">清除已完成任务</button>
    </div>
</template>

<script>
export default {
    name: 'MyFooter',
    props: {
        todoList: []
    },
    data() {
        return {
            
        };
    },

    mounted() {
        
    },
    computed: {
        doneSize() {
            return this.todoList.filter((item) => item.done).length || 0
        },
        allDone() {
            return !this.todoList.some((item) => !item.done)
        }
    },
    methods: {
        checkAll(event) {
            this.$bus.$emit('checkAll', event.target.checked)
        },
        clearDone() {
            this.$bus.$emit('clearDone')
        }
    },
};
</script>

<style lang="scss" scoped>
.todo-footer {
    height: 28px;
    line-height: 28px;
    padding-left: 6px;
    margin-top: 5px;
    button {
        float: right;
    }
}
</style>