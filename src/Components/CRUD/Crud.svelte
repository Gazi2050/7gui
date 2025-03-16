<script lang="ts">
    type Person = {
        name: string;
        surname: string;
    };

    const people = $state([
        { name: "Liam", surname: "Anderson" },
        { name: "Olivia", surname: "Brown" },
        { name: "Noah", surname: "Clark" },
        { name: "Emma", surname: "Davis" },
        { name: "Oliver", surname: "Evans" },
        { name: "Ava", surname: "Garcia" },
        { name: "Elijah", surname: "Harris" },
        { name: "Charlotte", surname: "Johnson" },
        { name: "William", surname: "Martinez" },
        { name: "Sophia", surname: "Miller" },
    ]);

    let selected = $state<Person>();
    let person = $state({ name: "", surname: "" });
</script>

<div
    class="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-6"
>
    <h2 class="text-xl font-semibold text-gray-800 mb-4">CRUD</h2>

    <div class="bg-white p-6 rounded-lg shadow-md w-full max-w-md space-y-4">
        <!-- Filter Input -->
        <div>
            <label for="" class="block text-sm font-medium text-gray-700"
                >Filter prefix:</label
            >
            <input
                type="text"
                class="w-full p-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none"
                placeholder="Type to filter..."
            />
        </div>

        <!-- Select Names -->
        <div>
            <label for="" class="block text-sm font-medium text-gray-700"
                >Names:</label
            >
            <select
                bind:value={selected}
                size="3"
                class="w-full p-3 border border-gray-300 rounded-lg bg-white shadow-sm text-gray-700 focus:ring-2 focus:ring-blue-500 focus:outline-none cursor-pointer"
            >
                {#each people as person}
                    <option
                        value={person}
                        class="p-2 text-gray-700 hover:bg-gray-100 cursor-pointer rounded-md"
                    >
                        {person.surname}, {person.name}
                    </option>
                {/each}
            </select>
        </div>

        <!-- Input Fields -->
        <div class="grid grid-cols-2 gap-4">
            <div>
                <label for="" class="block text-sm font-medium text-gray-700"
                    >Name:</label
                >
                <input
                    type="text"
                    bind:value={person.name}
                    class="w-full p-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none"
                />
            </div>
            <div>
                <label for="" class="block text-sm font-medium text-gray-700"
                    >Surname:</label
                >
                <input
                    type="text"
                    bind:value={person.surname}
                    class="w-full p-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:outline-none"
                />
            </div>
        </div>

        <!-- Action Buttons -->
        <div class="flex justify-between">
            <button
                class="px-4 py-2 bg-green-500 text-white rounded-lg hover:bg-green-600 transition"
                >Create</button
            >
            <button
                class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition"
                >Update</button
            >
            <button
                class="px-4 py-2 bg-red-500 text-white rounded-lg hover:bg-red-600 transition"
                >Delete</button
            >
        </div>
    </div>
</div>
