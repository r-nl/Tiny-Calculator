<script lang="ts">
	export let buttonLabel: string | number;

	import { createEventDispatcher } from "svelte";

	const dispatch = createEventDispatcher();

	function pressButton(button: string | number) {
		dispatch("buttonPressed", {
			button: button,
		});
	}
</script>

<button
	class="bg-slate-800 hover:bg-slate-900 rounded-xl p-4 cursor-pointer select-none flex items-center justify-center text-xl"
	on:click={() => pressButton(buttonLabel)}
>
	{buttonLabel}
</button>
