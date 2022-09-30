<template>
    <div class="todoList">
        <input 
            type="checkbox"
            @click="todoCheck"
        />
        <span
            :style="todo.checked ? 'text-decoration:line-through' : ''"
        >{{ todo.text }}</span>
        <button @click="todoDelete">제거</button>
    </div>
</template>

<script>
export default {
    props: {
        todo: {
            type: String,
            required: true
        }
    },
    methods: {
        todoCheck(e){
            this.$emit("todo-Check",{
                id: this.todo.id,
                checked: e.target.checked
            });
        },
        todoDelete(){
            this.$emit("todo-del", {
                id: this.todo.id
            });
        }
    }
}
</script>

<style>
    .todoList{display: flex; align-items: center; width: 100%; height: 50px; position: relative;}
    .todoList>span{display: inline-block; margin-left: 6px;}
    .todoList>button{position: absolute; right: 0; top: 50%; transform: translateY(-50%); background: orange; border: 0; color: #fff; font-size: 13px; font-weight: bold; padding: 5px 15px; border-radius: 5px; cursor: pointer;}
</style>