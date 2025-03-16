<script lang="ts">
    class Temperature {
        #c = $state(0);
        #f = $state(32);

        get c() {
            return this.#c;
        }

        set c(c) {
            this.#c = c;
            this.#f = c * (9 / 5) + 32;
        }

        get f() {
            return this.#f;
        }

        set f(f) {
            this.#f = f;
            this.#c = (f - 32) * (5 / 9);
        }
    }
    const temperature = new Temperature();
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <h2 class="text-xl font-semibold text-gray-800 mb-4">
        Temperature Converter
    </h2>

    <div class="flex items-center gap-4 p-6 bg-white rounded-lg shadow-md">
        <input
            type="number"
            class="w-20 px-3 py-2 text-center border border-gray-300 rounded-lg bg-gray-50 focus:outline-none focus:ring-2 focus:ring-red-500"
            bind:value={temperature.c}
        />
        <p class="text-sm text-gray-700">Celsius</p>

        <span class="text-gray-500">=</span>

        <input
            type="number"
            class="w-20 px-3 py-2 text-center border border-gray-300 rounded-lg bg-gray-50 focus:outline-none focus:ring-2 focus:ring-blue-500"
            bind:value={temperature.f}
        />
        <p class="text-sm text-gray-700">Fahrenheit</p>
    </div>
</div>
