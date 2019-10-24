<style>
	.payments {
		margin-top: 20px;
	}

	.options-container {
		position: fixed;
		bottom: 0;
		left: 0;
		width: 100%;
	}

	.options {
		display: flex;
		align-items: baseline;
		justify-content: center;
	}

	.add {
		margin-bottom: 20px;
		width: 85px;
		height: 45px;
		font-size: 41px;
		line-height: 1;
		background-color: #4872f0;
		color: white;
	}
</style>

<svelte:head>
	<title>Repayment Tracker</title>
</svelte:head>

<script>
	import ProgressBar from '../components/progress-bar.svelte';
	import Payment from '../components/payment.svelte';
	import Modal from '../components/modal.svelte';
	// progress bar to track progress
	const total = 1000;
	let nextId = 2;
	let showModal = false;

	// list payments
	let payments = [
		{
			id: 0,
			sum: 100,
			paymentDate: new Date('2019-06-23')
		}, {
			id: 1,
			sum: 150,
			paymentDate: new Date('2019-07-25')
		}
	]

	// button to add payment
	const addPayment = (value) => {
		const payment = {
			id: nextId++,
			sum: value ? value : (Math.random() * 100).toFixed(0),
			paymentDate: new Date()
		};

		payments = [payment, ...payments];
	};

	$: progress = payments.reduce((sum, payment) => {return sum + +payment.sum}, 0);
</script>

<ProgressBar bind:total bind:progress />

<h1>Repayment App</h1>

<div class="payments">
	{#each payments as payment (payment.id)}
		<Payment {...payment}/>
	{/each}
</div>

<div class="options-container">
	<div class="options">
		<button class="add" on:click={() => { showModal = true; }}>+</button>
	</div>
</div>

{#if showModal}
	<Modal on:close={() => { showModal = false; }} on:paymentConfirmed={(event) => { addPayment(event.detail.value); }} />
{/if}