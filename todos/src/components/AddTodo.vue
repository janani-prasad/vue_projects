<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" placeholder="Add a todo" />
            <input type="submit" value="Submit" class="btn btn-primary" />
        </form> 
    </div>
</template>
<script>
import {v4} from 'uuid';

export default {
    name: "AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault(); //to prevent the form from doing it's default behaviour and add a new todo
            const newTodo = {
                id: v4(),
                title: this.title,
                completed: false

            }
            //send new todo to app.vue
            this.$emit('add-todo',newTodo);
        }
    }
}
</script>
<style scoped>
@import'~bootstrap/dist/css/bootstrap.css';
form {
    display: flex;
}

input[type="text"] {
    flex: 10px;
    padding: 10px;
}

.btn-style {
    background: #fff;
}


</style>