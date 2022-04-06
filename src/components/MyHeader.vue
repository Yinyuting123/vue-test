<template>
    <div class="todo-header">
        <input 
            type="text" 
            @keyup.enter="addTodoItem"
            v-model="title" 
            placeholder="请输入你的任务名称，按回车键确认">
    </div>
</template>

<script>
import {nanoid} from 'nanoid'

export default {
    name: 'MyHeader',

    data() {
        return {
            title: ''
        };
    },

    mounted() {
        
    },

    methods: {
        addTodoItem(event) {
            if(this.title.trim().length > 0) {
                this.$emit('addTodoItem', {
                    id: nanoid(),
                    title: this.title,
                    done: false
                });
            } else {
                return alert('输入不能为空！')
            }
            this.title = ''
        },
    },
};
</script>

<style lang="scss" scoped>
.todo-header {
    input {
        width: 560px;
        height: 28px;
        font-style: 14px;
        border: 1px solid #ccc;
        border-radius: 4px;
        padding: 4px 7px;

        &:focus {
		    outline: none;
		    border-color: rgba(82, 168, 236, 0.8);
		    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
	    }
    }
}
</style>