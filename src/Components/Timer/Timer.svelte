<script lang="ts">
    let elapsed = $state(0);
    let duration = $state(10);
    let interval: number;

    function start() {
        interval = setInterval(() => {
            elapsed += 0.1;
            if (elapsed >= duration) {
                elapsed = duration;
                clearInterval(interval);
            }
        }, 100);
    }

    function reset() {
        elapsed = 0;
        start();
    }

    $effect(() => {
        if (!duration) return;
        start();
        return () => {
            clearInterval(interval);
        };
    });
</script>

<div class="flex items-center justify-center min-h-screen bg-gray-100">
    <div class="w-full max-w-sm p-6 bg-white rounded-2xl shadow-md">
        <div>
            <label
                for="elapsed"
                class="block text-sm font-medium text-gray-700"
            >
                Elapsed Time
            </label>
            <progress
                max={duration}
                value={elapsed}
                class="w-full h-2 rounded bg-gray-200"
            ></progress>
            <div class="mt-2 text-center text-sm text-gray-600">
                {elapsed.toFixed(1)}s
            </div>
        </div>

        <div class="mt-4">
            <label
                for="duration"
                class="block text-sm font-medium text-gray-700"
            >
                Duration
            </label>
            <input
                type="range"
                bind:value={duration}
                min="1"
                max="10"
                class="w-full accent-gray-900 cursor-pointer"
            />
            <div class="mt-1 text-xs text-gray-500">
                Set duration: {duration}s
            </div>
        </div>

        <button
            class="mt-6 w-full py-2 text-sm font-medium bg-gray-900 text-white rounded-lg shadow hover:bg-gray-800 transition"
            onclick={reset}
        >
            Reset
        </button>
    </div>
</div>
