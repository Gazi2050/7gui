<script lang="ts">
    let count: number = $state(0);
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <h2 class="text-xl font-semibold text-gray-800 mb-4">Counter</h2>

    <div class="flex items-center gap-4 p-4 bg-white rounded-lg shadow-md">
        <button
            onclick={() => count--}
            class="px-4 py-2 bg-red-500 text-white font-medium rounded-lg shadow hover:bg-red-600 transition"
        >
            Down
        </button>

        <input
            type="number"
            bind:value={count}
            disabled
            class="w-16 text-center border border-gray-300 rounded-lg p-2 bg-gray-50"
        />

        <button
            onclick={() => count++}
            class="px-4 py-2 bg-green-500 text-white font-medium rounded-lg shadow hover:bg-green-600 transition"
        >
            Up
        </button>
    </div>
</div>
