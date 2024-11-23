<script lang="ts">
    class Temperature {
        #c = $state(0);
        #f = $state(0);

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

<h2 class="text-center text-xl font-bold text-red-500 my-5">
    Temperature Converter
</h2>
<div
    class="flex justify-center items-center gap-3 border-2 rounded-lg w-[34%] mx-auto p-6 bg-gray-100"
>
    <input
        type="number"
        class="border-2 border-red-600 rounded p-3"
        bind:value={temperature.c}
    />
    <p class="text-lg font-semibold">Celsius</p>
    =
    <input
        type="number"
        class="border-2 border-blue-600 rounded p-3"
        bind:value={temperature.f}
    />
    <p class="text-lg font-semibold">Fahrenheit</p>
</div>
