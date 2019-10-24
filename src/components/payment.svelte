<style>
    .payment {
        display: block flex;
        width: 100%;
        align-items: center;
        justify-content: space-between;
        padding: 10px;
        background-color: rgb(216, 216, 216);
        border: 1px solid black;
    }

    .payment:not(:first-child) {
        margin-top: 10px;
    }
</style>

<script>
	import { quintOut } from 'svelte/easing';
	import { crossfade } from 'svelte/transition';

	const [send, receive] = crossfade({
		duration: d => Math.sqrt(d * 200),

		fallback(node, params) {
			const style = getComputedStyle(node);
			const transform = style.transform === 'none' ? '' : style.transform;

			return {
				duration: 600,
				easing: quintOut,
				css: t => `
					transform: ${transform} scale(${t});
					opacity: ${t}
				`
			};
		}
	});

    export let paymentDate = new Date();
    export let sum = 0;
    export let id;

    $: formattedDate = `${paymentDate.getFullYear()}/${paymentDate.getMonth() + 1}/${paymentDate.getDate()}`;
</script>

<div id={id} class="payment" in:receive={{key: id}}>
    <div class="sum">
        {sum}
    </div>
    <div class="payment-date">
        {formattedDate}
    </div>
</div>