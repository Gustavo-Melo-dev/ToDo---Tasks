<template>
    <div class="new-task">
        <input class="form-element" type="text" v-model="name" @keydown.enter="taskAdded" placeholder="Nova tarefa:">
        <button class="form-element" @click="taskAdded">+</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: ''
        }
    },
    methods: {
        taskAdded(){
            this.$emit('taskAdded', {name: this.name})
            this.name = ''
        }
    }
}
</script>

<style scoped>
    .new-task {
        margin: 35px;
    }
    .form-element {
        outline: none;
        font-size: 1.7rem;
        border: 1px solid #FFF;
        padding: 5px 10px 8px;
    }
    input.form-element {
        width: 450px;
        background: #FFF2;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
        color: white;
    }
    button.form-element {
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
    }
</style>