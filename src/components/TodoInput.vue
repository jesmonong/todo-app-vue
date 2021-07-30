<template>
<div>
<!-- Submit.prevent = prevent refresh -->
	<form @submit.prevent="addTodo"> 
		<label for="todo"></label>
		<input class="bg-grey-lighter text-grey-darker py-2 font-normal rounded text-grey-darkest border border-grey-lighter rounded-md font-bold text-center mb-2 " type="text" placeholder="Enter a todo" v-model="newTodo" />

		<button class='bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded'>Add Todo</button>
	</form>

	<div
		:class="{ 'line-through': todo.isComplete }"
		class='flex justify-center items-center'
		v-for="todo in todos"
		:key="todo.id"
		>
		<div>
			<p class='todo-item'>{{  todo.item }}</p>
		</div>
		
		<div>
			<button class= 'h-10 px-5 m-2 text-white transition-colors duration-150 bg-green-500 rounded-lg focus:shadow-outline hover:bg-green-600' v-if="todo.isComplete === false" @click="toggleTodo(todo)"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg></button>
			<button class= 'h-10 px-5 m-2 text-white transition-colors duration-150 bg-blue-400 rounded-lg focus:shadow-outline hover:bg-blue-600'  v-else @click="toggleTodo(todo)"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h10a8 8 0 018 8v2M3 10l6 6m-6-6l6-6"></path></svg></button>
			<button class= 'h-10 px-5 m-2 text-white transition-colors duration-150 bg-blue-400 rounded-lg focus:shadow-outline hover:bg-blue-600' @click="editTodo(todo)"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path></svg></button>
			<button class='h-10 px-5 m-2 text-white transition-colors duration-150 bg-red-500 rounded-lg focus:shadow-outline hover:bg-red-800' @click="removeTodo(todo)"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg></button>
		</div>
	</div>
	</div>
</template>

<script>
import {v4 as uuidv4} from "uuid"

export default {
	name: 'TodoInput',
	data() {
		return {
			newTodo: null,
			todos: [],
		};
	},
	methods: {
		addTodo() {
			const todo = {
				id:uuidv4(),
				item: '',
				isComplete: false,
			};
			todo.item = this.newTodo;
			if (this.newTodo){
			this.todos.push(todo);
			this.newTodo = ''; 
			}
			else {alert('Please input something')};
			
		},
		toggleTodo(clickedTodo) {
			this.todos.map((todo) => {
				if (todo.id === clickedTodo.id) {
					todo.isComplete = !todo.isComplete;
				}
			}); 
		},


		removeTodo(clickedTodo) {
			this.todos.map((todo) => {
				if (todo.id === clickedTodo.id) {
					this.todos.splice(this.todos.indexOf(clickedTodo), 1);
				}
			});
		},
		editTodo(clickedTodo) {
			this.todos.map((todo) => {
				if (todo.id === clickedTodo.id) {
					this.newTodo = clickedTodo.item;
					this.todos.splice(this.todos.indexOf(clickedTodo), 1);
				}
			});
		},
	},
};
</script>


