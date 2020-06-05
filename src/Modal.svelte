<script>
import { createEventDispatcher } from 'svelte'
const dispatch = createEventDispatcher()
// export let showModal
	let agreed=false

$: console.log('agree:', agreed)
</script>

<div class="backdrop">
 
</div>
<div class="modal">
  <header>
    <slot name="header" />
  </header>
  <div class="content">
    <slot name="content" />
  </div>
  <div class="disclaimer">
    <p>You need to agree before you leave</p>
    <button on:click={() => agreed = true}>Agree</button>
    <slot />
  </div>
  <footer>
    <div class="float-right">
      <slot name="footer" didAgree={agreed} >
        <button 
          on:click={() => dispatch("close")}
          disabled={!agreed}
        >
          confirm
        </button>
      </slot>
    </div>
  </footer>
</div>


<style>
  .backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(0, 0, 0, 0.75);
    z-index: 10;
  }

  .modal {
    padding: 1rem;
    position: fixed;
    top: 10vh;
    left: 10%;
    width: 80%;
    max-height: 80vh;
    background: white;
    border-radius: 5px;
    z-index: 100;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    overflow: scroll;
  }
  header {
    border-bottom: solid 1px grey;
    border-radius: 1px;
  }
  footer {
    border-top: solid 1px grey;
    padding-top: 1em;
    border-radius: 1px;
  }
  .float-right {
    float: right;

  }
  .content {
    color: navy;
  }

</style>
