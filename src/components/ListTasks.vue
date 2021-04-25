<template>
    <div class="listTasks">
        <template v-if="tasks.length">
            <Task v-for="(task, i) in tasks" :key="task.name" :task="task" @taskDeleted="$emit('taskDeleted', i)" @taskChanged="$emit('taskChanged', i)"></Task>
        </template>
        
        <p v-else class="no-task"><strong>Você está em dia com suas tarefas! :)</strong></p>
    </div>
</template>

<script>

import Task from './Task'

export default {
    components: {Task},
    props: {
        tasks:{
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
    .listTasks {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }
    .listTasks .task {
        margin: 10px;
    }
    .no-task {
        font-size: 1.7rem;
    }
</style>