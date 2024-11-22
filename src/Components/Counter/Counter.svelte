<script lang="ts">
    let count: number = $state(0);
    // let count = 0;
</script>

<h2 class="text-center text-xl font-bold text-red-500 my-5">Counter</h2>
<div
    class="flex justify-center items-center gap-3 border-2 rounded-lg w-[20%] mx-auto p-7 bg-gray-100"
>
    <button
        onclick={() => count--}
        class="border rounded p-3 bg-red-600 text-white">Down</button
    >
    <input
        type="number"
        bind:value={count}
        class="border rounded p-3"
        disabled
    />
    <button
        onclick={() => count++}
        class="border rounded p-3 bg-green-600 text-white">Up</button
    >
</div>
