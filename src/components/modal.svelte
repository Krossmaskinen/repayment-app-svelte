<style>
    .modal-background {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: #000;
        opacity: 0.7;
        z-index: 99;
    }

    .modal {
        z-index: 100;
        background-color: #fff;
        width: 100%;
        min-height: 180px;
        position: fixed;
        bottom: 0;
        left: 0;
        padding: 20px;
    }

    .modal-options {
        display: block flex;
        align-items: center;
        justify-content: space-between;
        margin-top: 20px;
    }

    .confirm {
        background-color: rgb(108, 230, 92);
        color: #fff;
    }

    .cancel {
        background-color: rgb(235, 83, 83);
        color: #fff;
    }

    button {
        font-size: 41px;
		line-height: 1;
		width: 85px;
		height: 45px;
    }
</style>

<script>
    import { createEventDispatcher } from 'svelte';
    import { slide, fade } from 'svelte/transition';

    const dispatch = createEventDispatcher();
    let value = 4000;

    const closeModal = () => {
        value = 4000;

        dispatch('close');
    };

    const confirmPayment = () => {
        dispatch('paymentConfirmed', {value});

        closeModal();
    };
</script>

<div class="modal-background" on:click={() => {dispatch('close')}}></div>

<div class="modal" in:slide out:fade={{duration: 100}}>
    <div class="header">
        <h2>New payment</h2>
    </div>
    <div>
        <input type="text" bind:value />
        <div class="modal-options">
            <button class="confirm" on:click={confirmPayment}>✓</button>
            <button class="cancel" on:click={() => {dispatch('close')}}>X</button>
        </div>
    </div>
</div>