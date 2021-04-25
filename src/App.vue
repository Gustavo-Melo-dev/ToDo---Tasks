<template>
	<div id="app">
		<h1>Tarefas</h1>
		<ProgressTasks :progress="progress"></ProgressTasks>
		<InputTasks @taskAdded="addTask" ></InputTasks>
		<ListTasks :tasks="tasks" @taskDeleted="deleteTask" @taskChanged="changedTask"></ListTasks>
	</div>
</template>

<script>

import ProgressTasks from './components/ProgressTasks'
import InputTasks from './components/InputTasks'
import ListTasks from './components/ListTasks'

export default {
	components: {ProgressTasks, InputTasks, ListTasks},
	data() {
		return {
			tasks: []
		}
	},
	computed: {
		progress(){
			const total = this.tasks.length
			const done = this.tasks.filter(done => !done.pending).length
			return Math.round(((done / total) * 100) || 0)
		}
	},
	watch: {
		tasks:{
			deep: true,
			handler() {
				localStorage.setItem('tasks', JSON.stringify(this.tasks))
			}
		}
	},
	methods: {
		addTask(task){
			const verifyName = t => t.name === task.name
			const reallyNew = this.tasks.filter(verifyName).length == 0
			if(reallyNew) {
				this.tasks.push({
					name: task.name,
					pending: task.pending || true
				})	
			}
		},
		deleteTask(i){
			this.tasks.splice(i, 1)
		},
		changedTask(i){
			this.tasks[i].pending = !this.tasks[i].pending
		}
	},
		created(){
			const json = localStorage.getItem('tasks')
			const array = JSON.parse(json)
			this.tasks = Array.isArray(array) ? array : []
		
		}
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, #185a9d, #43cea2);
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
	.progress-bar {
        background: black;
    }
</style>
