<template>
	<!--
	Awesome Exercise 1 - Vue.js Basics

	OK 1) Create data properties for name and age
	OK 2) Bind these properties to the two input fields
	OK 3) Display the name and age in the beige box (first line in bold)
	OK 4) Use a computed property to display the age plus 10 years (second line in bold)
	OK 5) Display the number of characters in the name (third line)
	OK 6) Use a filter to display the name in upper case (fourth line)
	OK 7) Only show the beige box if both a name and age have been entered, otherwise, show the red box ("Please enter a name and age.")
	Ok 8) Use v-show to only show the error messages next to the fields if the name is longer than 15 characters and the age is greater than 100
	OK 9) Add the class "error" to the input fields if they break the same rules
	OK 10) When the "Generate Random Person" button is clicked, generated a random name (from an array you create) and a random age from 1 - 100. These new values should be reflected everywhere in the view
	OK 11) Create a directive which auto-focuses the name field when the page loads
	OK 12) Make it so a random person is generated when the page first loads

	-->
  <q-page padding>
  	<div class="form q-mb-lg">
	  	<div class="row q-mb-md">
	  		<label>Name:</label>
	  		<input 
				type="text" 
				v-model="name"
				:class="{ 'error' : errorName }"
				v-autofocus
			> 
	  		<label 
				v-show="errorName"
				class="error"
			>Please enter 15 characters or less</label>
	  	</div>
	  	<div class="row q-mb-md">
		  	<label>Age:</label>
		  	<input 
				type="number" 
				v-model="age"
				:class="{ 'error' : errorAge }"
			>
	  		<label 
				v-show="errorAge"
				class="error"
			>Please enter an age between 1 - 100</label>
		  </div>
		  <div class="row">
		  	<button
				@click="generateRandomPerson"
			>Generate Random Person</button>
		  </div>
  	</div>
  	<div
		v-if="isThereANameAndAnAge" 
		class="description q-mb-lg"
	>
  		<p>My name is <b>{{ name }}</b> and I'm <b>{{ age }}</b> years old.</p>
  		<p>In 10 years I will be <b>{{ agePlusTen }}</b>.</p>
  		<p>My name is <b>{{ numOfChars }}</b> characters long.</p>
  		<p>My name in uppercase is <b>{{ name | toUpperCase }}</b>.</p>
  	</div>
	<div
		v-else 
		class="no-details"
	>
		<p>Please enter a name and age.</p>
	</div>
  </q-page>
</template>

<script>
	export default {
		data() {
			return {
				name: '',
				age: 0,
				names: ['Jennifer', 'Carlos', 'Pedro']
			}
		},
		computed: {
			agePlusTen() {
				return Number(this.age) + 10;
			},
			numOfChars() {
				return this.name.length;
			},
			isThereANameAndAnAge() {
				if(this.name.length > 0 && this.age > 0) {
					return true;
				} else {
					return false;
				}
			},
			errorName() {
				return this.name.length > 15 || !this.name.length;
			},
			errorAge() {
				return 0 >= this.age || this.age > 100;
			}
		},
		methods: {
			generateRandomPerson() {
				this.name = this.names[Math.floor(Math.random() * this.names.length)];
				this.age = Math.floor(Math.random() * 100)
			}
		},
		filters: {
			toUpperCase(value) {
				return value.toUpperCase();
			}
		},
		directives: {
			autofocus: {
				inserted(el) {
					el.focus()
				}
			}
		},
		mounted() {
			this.name = this.names[Math.floor(Math.random() * this.names.length)];
			this.age = Math.floor(Math.random() * 100)
		}
	}
</script>

<style>
	.form {
		background: #eee;
		padding: 10px;
	}
	label {
		min-width: 70px;
	}
	label.error {
		font-size: 13px;
		color: red;
		margin-left: 5px;
		margin-top: 3px;
	}
	input {
		border: 1px solid #ccc;
	}
	input.error {
		border: 1px solid red;
		background: pink;
	}
	.description {
		background: antiquewhite;
		padding: 20px 20px 7px;
	}
	.no-details {
		background: lightcoral;
		padding: 20px 20px 7px;
	}
</style>
