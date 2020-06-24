<template>
    <div>
        <form action="" @submit="addTodo">
            <input type="text" name="title" v-model="title" placeholder="Add todo ...">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
//import { v4 as uuidv4 } from 'uuid'; //for id

export default {
    name: "AddTodo",
    data () {
        return {
            title: '',
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                // id : uuidv4(),
                title: this.title,
                completed: false,
            }
            //Setup up to parent
            this.$emit("add-todo", newTodo);
            this.title = '';
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }
    input[type="text"] {
        flex: 10;
        padding: 5px;
    }
    input[type="submit"] {
        flex: 2;
    }
</style>