<template>
	<div id="app">

		<h1>Tarefas</h1>
		<TaskProgress :progress="progress" /> 
		<div class="form-row">
			<!-- <input type="text" :value="teste"> -->
			<!-- <input type="text"> -->
			<!-- <button>+</button> -->
		</div>
		<NewTask @taskAdded = "addTask" /> 
		<TaskGrid :tasks="tasks" @taskRemoved = "removeTask" />
	</div>
</template>

<script>
import TaskGrid from './components/TaskGrid.vue'
import NewTask from './components/NewTask.vue'
// import ProgressBar from './components/ProgressBar.vue'

import Vue from 'vue'
// import Vuetify from 'vuetify'
// Vue.use(Vuetify)

// import 'vuetify/dist/vuetify.min.css';

import TaskProgress from './components/TaskProgress.vue'


export default {
	components: { TaskProgress, TaskGrid, NewTask },
	data(){
		return{
			tasks:[
				{name:'Lavar louça', pending: false},
				{name:'Fazer compras', pending: true}
			]
		}
	},
	computed: {
		progress(){
			const total = this.tasks.length
			const done = this.tasks.filter(t => !t.pending).length 
			return Math.round(done / total * 100) || 0
		}
	},
	methods: {
		addTask(task){
			const sameName = t => t.name === task.name 
			const reallyNew = this.tasks.filter(sameName).length == 0
			if (reallyNew) {
				this.tasks.push({
					name: task.name,
					pending: task.pending || true
				})
			}else{
				alert('Este item ja existe!')
			}
		},
		removeTask(task){
			// console.log('Evento disparado!')
			this.tasks.splice(task, 1);
		}
	}

}
</script>

<style>

	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
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

	.tasks-progress{
		position: relative;
		width: 80%;
		border: 1px solid #FFF;
		color: #FFF;
		border-radius: 8px;
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	.progress-bar{
		position: absolute;
		border-radius: 8px;
		height: 100%;
		background-color: #4CAF50;
		align-self: flex-start;
	}
	.progress-value{
		z-index: 1;
		font-size: 1.5rem;
	}
	
</style>
