<style>
    .progress-container {
        position: relative;
        width: 100%;
        height: 25px;
        background-color: rgb(244, 244, 244);
        border: 1px solid black;
        overflow: hidden;
    }

    .progress {
        position: absolute;
        top: 0;
        left: 0;
        height: 23px;
        background-color: rgb(167, 238, 127);
    }
</style>

<script>
    export let total = 100;
    export let progress = 0;

    $: width = (progress/total) * 100;
    // container
    // progress
</script>

{progress}/{total}
<div class="progress-container">
    <div class="progress" style='width: {width}%'></div>
</div>