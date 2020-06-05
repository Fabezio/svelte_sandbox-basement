<script>
  import { createEventDispatcher } from 'svelte'
  export let title
  export let price
  export let author
  export let bestseller = false
  // export let product
  

  const dispatch = createEventDispatcher()

  
</script>

<article>
  <div>{author}</div>
  <div>{title}</div>
  <div>${price}</div>
  {#if bestseller}
  <div>Bestseller</div>
  {/if}
  
  <button on:click={(e) => dispatch('add-to-cart', e)}>Add to cart</button>
  <button on:click={(e) => dispatch('delete', e)}>Delete</button>
</article>

<style>
div {
		color: navy;
		text-transform: uppercase;
		font-size: 2em;
		font-weight: 100;
	}
button {
  background: #077;
  color: white;
  border-radius: 5px;
  padding: .5em 1em;
}
</style>