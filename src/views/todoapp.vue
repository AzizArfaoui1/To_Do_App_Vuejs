
<template>
	<main class="todoapp">
		<section class="create-todo">
			<h3>CREATE A TODO</h3>

			<form id="new-todo-form" @submit.prevent="addTodo">
				<h4>What's on your todo list?</h4>
				<input 
					type="text" 
					name="content" 
					id="content" 
					placeholder="Enter your todo"
					v-model="input_content" />
				
				<h4>Pick a category</h4>
				<div class="options">

					<label>
						<input 
							type="radio" 
							name="category" 
							id="category1" 
							value="business"
							v-model="input_category" />
						<span class="bubble business"></span>
						<div>Work</div>
					</label>

					<label>
						<input 
							type="radio" 
							name="category" 
							id="category2" 
							value="personal"
							v-model="input_category" />
						<span class="bubble personal"></span>
						<div>Personal</div>
					</label>

				</div>

				<input type="submit" value="Add todo" />
			</form>
		</section>

		<section class="todo-list">
			<h3>TODO LIST</h3>
			<div class="list" id="todo-list">

				<!-- Update the div element inside the v-for loop with a unique key -->
<div v-for="todo in todos_asc" :key="todo.id" :class="`todo-item ${todo.done && 'done'}`">
    <label>
        <input type="checkbox" v-model="todo.done" />
        <span :class="`bubble ${
            todo.category == 'business' 
                ? 'business' 
                : 'personal'
        }`"></span>
    </label>

    <div class="todo-content">
        <input type="text" v-model="todo.content" />
    </div>

    <div class="actions">
        <button class="delete" @click="removeTodo(todo)">Delete</button>
    </div>
</div>


			</div>
		</section>

	</main>
</template>

<!-- ... -->
<script>
import { ref} from 'vue';

  

export default {

  name: 'todoappView',
  components: {},
  setup() {
    const todos = ref([]);
    const input_content = ref('');
    const input_category = ref(null);


    // ... (other parts of the setup function)

    const addTodo = () => {
      if (input_content.value.trim() === '' || input_category.value === null) {
        return;
      }

      const newTodo = {
        content: input_content.value,
        category: input_category.value,
        done: false,
        editable: false,
        createdAt: new Date().getTime(),
      };

      todos.value.push(newTodo);
    };

    const removeTodo = (todo) => {
      todos.value = todos.value.filter((t) => t !== todo);
    };

    // ... (other parts of the setup function)

    return {
      input_content,
      input_category,
      todos,
    
      addTodo,
      removeTodo,
    };
  },
};
</script>
<!-- ... -->
