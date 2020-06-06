<script>
	import { tick } from 'svelte'
	import Product from './Product.svelte'
	import Modal from './Modal.svelte'
	let text = 'You wanna uppercase this?'
	let products = [
		{
			// id: "1",
			author: "Jules Verne",
			title: "Journey to the Earth Core",
			// bestseller:true,
			price: 4.95
		}
	]
	let showModal=false
	let closeable = false
		// let title
	function addToCart(e) {console.log(e.detail)}
	function deleteFromCart(e) {console.log(e.detail)}

	  function transform(event) {
	  if (event.which !== 9) {
		  return;
	  }
	  event.preventDefault();

	  const selectionStart = event.target.selectionStart;
	  const selectionEnd = event.target.selectionEnd;
	  const value = event.target.value

	  text = value.slice(0, selectionStart) +
			 value.slice(selectionStart, selectionEnd).toUpperCase() +
			 value.slice(selectionEnd);

	  tick().then(() => {
		event.target.selectionStart = selectionStart;
	    event.target.selectionEnd = selectionEnd;
	  });

      // Will not work!
	//   event.target.selectionStart = selectionStart;
	//   event.target.selectionEnd = selectionEnd;
  }

</script>

<main>
	{#each products as product}
	<Product 
		{...product}
		on:add-to-cart={addToCart}
		on:delete={deleteFromCart}
	 />
	{/each}

	<button on:click={() => showModal = true } >show modal</button>
	{#if showModal}
	<Modal 
		on:cancel={() => showModal = false}
		on:close={() => showModal = false}
		let:didAgree={ closeable}
	>
		<h1 slot="header">Hello!</h1>
		<p slot="content">Good to see ya!</p>
		<button 
			slot="footer" 
			on:click={() => showModal = false } 
			disabled={!closeable} 
		>Close</button>
	 </Modal>
	 {/if}
	<br>
	<textarea 
		cols="50" 
		rows="3" 
		value={text}
		on:keydown={transform}
	></textarea>
	 
</main>

<style>
	main {
		/* text-align: center; */
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>