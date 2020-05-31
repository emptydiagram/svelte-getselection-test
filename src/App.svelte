<script>
	export let name;
  import { afterUpdate } from "svelte";

	afterUpdate(() => {
    let theInput = document.getElementById("the-input");
    if (theInput && isToggling) {
      isToggling = false;
      console.log("  aU!!!  selStart = ", selStart);
      theInput.selectionStart = selStart;
      theInput.selectionEnd = selStart;
      theInput.focus();
    }
	});


  let isEditing = false;
  let isToggling = false;
  let inputValue = "this is some text that you can click on";
  let selStart;


  document.addEventListener('selectionchange', (ev) => {
    let sel = document.getSelection();
    let theSpan = document.getElementById("the-span");
    if (theSpan && sel.anchorNode === theSpan.firstChild) {
      selStart = sel.anchorOffset;
      isEditing = true;
      isToggling = true;
    } else {
      console.log("skipping OSC");
    }
  });

  function handleBlur(ev) {
    isEditing = false;
  }

</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {name}!</h1>

{#if isEditing}
  <input id="the-input" type="text" bind:value={inputValue} on:blur={handleBlur} />
{:else}
  <span id="the-span">{inputValue}</span>
{/if}
