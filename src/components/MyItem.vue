<template>
    <li class="todo-item">
        <label>
            <input type="checkbox" :checked="todoItem.done" @change="handleCheck(todoItem.id)">
            <input 
                v-if="todoItem.isEdit" 
                type="text" 
                :value="todoItem.title"
                @keydown.enter="handleBlur(todoItem,$event)"
                @blur="handleBlur(todoItem,$event)"
                ref="inputTitle">
            <span v-else>{{todoItem.title}}</span>
        </label>
        <button class="btn btn-danger" @click="deleteTodo(todoItem.id)">删除</button>
        <button class="btn btn-edit" @click="editTodo(todoItem)">编辑</button>
    </li>
</template>

<script>
export default {
    name: 'MyItem',
    props: {
        todoItem: {}
    },
    data() {
        return {
            
        };
    },

    mounted() {
        
    },

    methods: {
        handleCheck(todoId) {
            this.$bus.$emit('checkTodo', todoId)
        },
        deleteTodo(todoId) {
            this.$bus.$emit('deleteTodo', todoId)
        },
        editTodo(todo) {
            if(todo.hasOwnProperty('isEdit')) {
                todo.isEdit = true
            } else {
                this.$set(todo, 'isEdit', true);   
            }
            this.$nextTick(() => {
                this.$refs.inputTitle.focus()
            })
        },
        handleBlur(todo, event) {
            todo.isEdit = false
            if(!event.target.value.trim()) return alert('输入不能为空！')
            this.$bus.$emit('updateTodo', todo.id, event.target.value)
        }
    },
};
</script>

<style lang="scss" scoped>
.todo-item {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;

    label {
        float: left;
        cursor: pointer;

        input {
            vertical-align: middle;
		    margin-right: 6px;
		    position: relative;
		    top: -1px;
        }
    }
    button {
        display: none;
        float: right;
        margin-top: 3px;
    }

    &:hover {
        background-color: #ddd;

        button {
            display: block;
        }
    }

    &:before {
        content: initial;
    }

    &:last-child {
        border: none;
    }
}
</style>