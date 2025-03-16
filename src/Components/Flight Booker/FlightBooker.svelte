<script lang="ts">
    type Options = "one-way" | "return";

    function getDate() {
        const date = new Date();
        const [month, day, year] = date
            .toLocaleDateString("en-US", {
                year: "numeric",
                month: "2-digit",
                day: "2-digit",
            })
            .split("/");
        return `${year}-${month}-${day}`;
    }

    function handleSubmit(e: Event) {
        e.preventDefault();
        alert(`You have a ${selected} flight on ${startDate}`);
    }

    let selected = $state<Options>("one-way");
    let startDate = $state(getDate());
    let returnDate = $state(getDate());
</script>

<div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <h2 class="text-xl font-semibold text-gray-800 mb-4">Flight Booker</h2>

    <form
        onsubmit={handleSubmit}
        class="w-full max-w-sm p-6 bg-white rounded-lg shadow-md space-y-4"
    >
        <div>
            <label class="block text-sm font-medium text-gray-700 mb-1"
                >Flight Type</label
            >
            <select
                bind:value={selected}
                class="w-full p-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"
            >
                <option value="one-way">One-way</option>
                <option value="return">Return Flight</option>
            </select>
        </div>

        <div>
            <label class="block text-sm font-medium text-gray-700 mb-1"
                >Start Date</label
            >
            <input
                type="date"
                min={getDate()}
                bind:value={startDate}
                required
                class="w-full p-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"
            />
        </div>

        <div>
            <label class="block text-sm font-medium text-gray-700 mb-1"
                >Return Date</label
            >
            <input
                type="date"
                min={startDate}
                bind:value={returnDate}
                disabled={selected !== "return"}
                required
                class="w-full p-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500"
            />
        </div>

        <button
            type="submit"
            disabled={!startDate ||
                (selected === "return" && returnDate < startDate)}
            class="w-full py-2 bg-blue-600 text-white font-medium rounded-lg shadow hover:bg-blue-700 transition"
        >
            Book Flight
        </button>
    </form>
</div>
