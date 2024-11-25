<script lang="ts">
    type Options = "one-way" | "return";

    function getDate() {
        const date = new Date();
        const [month, day, year] = date
            .toLocaleDateString("en-Us", {
                year: "numeric",
                month: "2-digit",
                day: "2-digit",
            })
            .split("/");
        return `${day}-${month}-${year}`;
    }

    function handleSubmit(e: Event) {
        e.preventDefault();
        alert(`You have a ${selected} flight on ${startDate}`);
    }

    let selected = $state<Options>("one-way");
    let startDate = $state(getDate());
    let returnDate = $state(getDate());

    $inspect({ selected, startDate, returnDate });
</script>

<h2 class="text-center text-xl font-bold text-red-500 my-5">Flight Booker</h2>
<form
    onsubmit={handleSubmit}
    class="max-w-md mx-auto p-6 bg-white shadow-lg rounded-md space-y-6"
>
    <div>
        <label
            for="flight-type"
            class="block text-sm font-medium text-gray-700 mb-1"
            >Flight Type</label
        >
        <select
            id="flight-type"
            bind:value={selected}
            class="w-full p-2.5 border rounded-md text-gray-700 focus:ring focus:ring-blue-300 focus:outline-none"
        >
            <option value="one-way">One-way</option>
            <option value="return">Return Flight</option>
        </select>
    </div>
    <div>
        <label
            for="start-date"
            class="block text-sm font-medium text-gray-700 mb-1"
            >Select the Start Date</label
        >
        <input
            id="start-date"
            type="date"
            min={getDate()}
            bind:value={startDate}
            required
            class="w-full p-2.5 border rounded-md text-gray-700 focus:ring focus:ring-blue-300 focus:outline-none"
        />
    </div>
    <div>
        <label
            for="return-date"
            class="block text-sm font-medium text-gray-700 mb-1"
            >Select the Return Date</label
        >
        <input
            id="return-date"
            type="date"
            min={getDate()}
            bind:value={returnDate}
            disabled={selected != "return"}
            required
            class="w-full p-2.5 border rounded-md text-gray-700 focus:ring focus:ring-blue-300 focus:outline-none"
        />
    </div>
    <button
        type="submit"
        disabled={!startDate ||
            (selected === "return" && returnDate < startDate)}
        class="w-full bg-red-500 text-white py-2 px-4 rounded-md hover:bg-red-600 transition duration-300 focus:outline-none focus:ring focus:ring-red-300"
    >
        Book
    </button>
</form>
