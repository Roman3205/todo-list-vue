<script>

export default {
    data() {
        return {
            newTodo: ``,
            todos: [
                {title: 'Сделать ДЗ', isDone: true},
                {title: 'Полить цветы', isDone: false},
                {title: 'Покормить собаку', isDone: false},
            ]
        }
    },

    methods: {
        toggle(item){
            item.isDone = !item.isDone
        },
        add() {
            if(!this.newTodo){
                return
            }
            this.todos.push({
                title: this.newTodo,
                isDone: false
            })
            this.newTodo = ``
        },
        remove(index) {
            this.todos.splice(index, 1)
        }
    }
}
</script>

<template>
    <div class="todo-list">
        <div class="input-group mb-3">
            <input v-model="newTodo" type="text" class="form-control">
            <button class="btn btn-outline-secondary" type="button" @click="add">
                Добавить
            </button>
        </div>
        <ul class="list-group">
            <li class="list-group-item" 
            v-for="(item, index) in todos"
            @click="toggle(item)"
            :class="{
                done: item.isDone
            }">
                <div class="input-group">
                    <div class="input-group-text">
                        <input v-model="item.isDone" class="form-check-input mt-0" type="checkbox">
                    </div>
                    <span class="input-group-text todo-title">
                        {{ item.title }}
                    </span>
                    <button class="btn btn-outline-secondary" type="button" @click="remove(index)">
                        X
                    </button>
                </div>
            </li>
        </ul>
    </div>
</template>

<style>
    .todo-title {
        flex: 1;
    }
    .input-group {
        cursor: pointer;
    }
    .done .todo-title {
        text-decoration: line-through;
    }
    .todo-list {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
    }
</style>