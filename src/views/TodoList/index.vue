<template>
    <div class="todo__container">
        <div class="todo__wrap">
            <MyHeader @addTodoItem="addTodoItem"/>
            <MyList :todoList="todoList"/>
            <MyFooter :todoList="todoList"/>
        </div>
    </div>
</template>

<script>
import MyHeader from '../../components/MyHeader'
import MyFooter from '../../components/MyFooter'
import MyList from '../../components/MyList'

export default {
    name: 'TodoList',
    components: {
        MyHeader,
        MyFooter,
        MyList
    },

    data() {
        return {
            todoList: []
        };
    },

    mounted() {
        this.$bus.$on('checkTodo', this.checkTodo)
        this.$bus.$on('deleteTodo', this.deleteTodo)
        this.$bus.$on('updateTodo', this.updateTodo)
        this.$bus.$on('checkAll', this.checkAll)
        this.$bus.$on('clearDone', this.clearDone)
        this.getTodoList()
    },
    watch: {
        todoList: {
            deep: true,
            handler(val) {
                localStorage.setItem('todoList', JSON.stringify(val))
            }
        }
    },
    methods: {
        addTodoItem(val) {
            this.todoList.unshift(val)
        },
        getTodoList() {
            this.todoList = JSON.parse(localStorage.getItem('todoList')) || []
        },
        checkTodo(todoId) {
            this.todoList.forEach(item => {
                if(item.id === todoId) {
                    item.done = !item.done
                }
            })
        },
        deleteTodo(todoId) {
            this.todoList = this.todoList.filter(item => item.id !== todoId)
        },
        updateTodo(todoId, value) {
            let todo = this.todoList.find(todo => todo.id === todoId)
            todo.title = value
        },
        checkAll(checked) {
            this.todoList.forEach(todo => todo.done = checked)
        },
        clearDone() {
            this.todoList = this.todoList.filter(todo => !todo.done)
        }
    },
};
</script>

<style lang="scss">
.todo{
    &__container {
        width: 600px;
        margin: 0 auto;
    } 
    
    &__wrap {
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 5px;

        .btn {
            color: #fff;
            padding: 4px 10px;
            margin-bottom: 0;
            font-size: 14px;
		    line-height: 20px;
		    text-align: center;
            vertical-align: middle;
            cursor: pointer;
		    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
            border-radius: 4px;
        }

        .btn-danger {
            background-color: #da4f49;
            border: 1px solid #bd362f;
        }

        .btn-edit {
            background-color: skyblue;
		    border: 1px solid rgb(103, 159, 180);
            margin-right: 5PX;
        }
    }
}
</style>