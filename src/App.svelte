<script>
	export let name;
  import { afterUpdate } from "svelte";

	afterUpdate(() => {
    let theInput = document.getElementById("the-input");
    if (theInput) {
      console.log("  aU!!!  selStart = ", selStart);
      theInput.selectionStart = selStart;
      theInput.selectionEnd = selStart;
      theInput.focus();
    }
	});


  let isEditing = false;
  let inputValue = "this is some text that you can click on";
  let selStart;


  function handleMousedown(ev) {
    console.log(" hmd: ", ev);

    /*
    let theSpan = document.getElementById("the-span");
    inputValue = theSpan.innerHTML;
     */

    let sel = window.getSelection();
    console.log(" hM, anchorOffset = ", sel.anchorOffset);
    selStart = sel.anchorOffset;

    // theInput.style.display = 'inline';
    // ev.target.style.display = 'none';
    isEditing = true;
  }
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {name}!</h1>

{#if isEditing}
  <input id="the-input" type="text" bind:value={inputValue} />
{:else}
  <span id="the-span" on:mousedown={handleMousedown}>{inputValue}</span>
{/if}
