<script>
    const links = [
        { name: "Counter", path: "/counter" },
        { name: "Temperature Converter", path: "/temperatureConverter" },
        { name: "Flight Booker", path: "/flightBooker" },
        { name: "Timer", path: "/timer" },
        { name: "CRUD", path: "/crud" },
        { name: "Circle Drawer", path: "/circledrawer" },
        { name: "Cells", path: "/cells" },
    ];
</script>

<div class="flex justify-center items-center h-screen w-full bg-gray-100">
    <div class="text-center">
        <h1 class="text-3xl font-bold text-red-500 my-5">
            7 GUIs (Graphical User Interface)
        </h1>

        <div class="flex flex-wrap gap-4 justify-center">
            {#each links as link}
                <a
                    href={link.path}
                    class="px-6 py-2 bg-gray-900 text-white font-medium rounded-lg shadow hover:bg-gray-800 transition"
                >
                    {link.name}
                </a>
            {/each}
        </div>
    </div>
</div>
