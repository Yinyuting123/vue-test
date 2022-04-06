<template>
    <ul class="todo-main">
        <MyItem v-for="todoItem in todoList" :key="todoItem.id" :todoItem="todoItem"/>
    </ul>
</template>

<script>
import MyItem from './MyItem'
export default {
    name: 'MyList',
    components: {MyItem},
    props: {
        todoList: []
    },
    data() {
        return {
            
        };
    },

    mounted() {
        
    },

    methods: {
        
    },
};
</script>

<style lang="scss" scoped>
.todo-main {
    margin-left: 0;
    padding: 0;
    border: 1px solid #ddd;
    border-radius: 2px;
}
</style>