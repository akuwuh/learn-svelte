<script>
	import Modal from './Modal.svelte';
	import AddPersonForm from './AddPersonForm.svelte';

	let firstName = "Isaac"; 
	let lastName = "Nguyen";
	let beltColour = 'black';

	$: fullName = `${firstName} ${lastName}`;
	$: {
		console.log(beltColour); // watches wtv variable is inside statement. if variable is updated, the statement is executed
		console.log(fullName); //use curly braces to group multiple statements
	}
	const handleClick = () => {
		beltColour = beltColour === 'black' ? 'white' : 'black';
	};
	const handleInput = (e) => {
		beltColour = e.target.value;
	}


	// Loops
	let people = [
		{name : 'Yoshi', beltColour: 'black', age: 25, id: 1},
		{name : 'Mario', beltColour: 'orange', age: 45, id: 2},
		{name : 'Luigi', beltColour: 'brown', age: 35, id: 3}
	];

	// Inline Event Handlers
	const handleDelete = (id) => { 
		people = people.filter(person => person.id != id);
	}

	// Conditionals
	let num = 5;

	let showModal = false;
	
	const toggleModal = () => {
		showModal = !showModal;
	};

	const addPersonHandler = (e) => {
		console.log(e.detail);
		const person = e.detail;

		people = [people, ...people];
		showModal = false;
	};

</script>

<!-- Conditionals -->

<!-- Components + Props -->
<Modal message="Sign Up for Offers!" {showModal} on:click={toggleModal}> 
	<AddPersonForm on:addPerson={addPersonHandler}/>
</Modal>


<main>

	<h1>Svelte Basics</h1>
	<!-- Basics -->
	<p>{fullName} - {beltColour} belt</p>
	<input type="text" bind:value={firstName}> 
	<input type="text" bind:value={lastName}>
	<input type="text" bind:value={beltColour}>


	<h1>Loops + Inline Event Handlers</h1>

	<!-- Loops -->
	{#each people as person (person.id)} 
		<div>
			<h4>{person.name}</h4>
			<!-- Conditionals -->
			{#if person.beltColour === 'black'}
				<p><strong>Master Ninja</strong></p>
			{/if}

			<p>{person.age} years old, {person.beltColour} belt.</p>
			<!-- Inline Event Handlers -->
			<button on:click={handleDelete(person.id)}>Delete</button>
			
		</div>
	{:else}
		<p>There are no people to display..</p>
	{/each}
	
	<!-- Event Forwarding + Props -->

	<button on:click={toggleModal}>Open Modal</button>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>