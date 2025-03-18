<script lang="ts">
    type Circle = {
        id: string;
        cx: number;
        cy: number;
        r: number;
    };

    type Status = "drawing" | "editing";

    let status = $state<Status>("drawing");
    let circles = $state<Circle[]>([]);
    let selected = $state<Circle | null>(null);
    // svelte-ignore non_reactive_update
    let snapshots: Circle[][] = [];
    let history = $state(-1);

    function drawCircle(e: MouseEvent) {
        if (status === "editing") return;

        const svgEl = e.currentTarget as SVGSVGElement;
        const { left, top } = svgEl.getBoundingClientRect();

        const newCircle: Circle = {
            id: crypto.randomUUID(),
            cx: +(e.clientX - left).toFixed(),
            cy: +(e.clientY - top).toFixed(),
            r: 40,
        };

        snapshot();
        circles = [...circles, newCircle];
        selected = newCircle;
    }

    function undo() {
        if (history > 0) {
            history--;
            circles = [...snapshots[history]];
        }
    }

    function redo() {
        if (history < snapshots.length - 1) {
            history++;
            circles = [...snapshots[history]];
        }
    }

    function snapshot() {
        snapshots = snapshots.slice(0, history + 1);
        snapshots.push([...circles]);
        history++;
    }

    function handleSelect(circle: Circle, e: MouseEvent) {
        e.stopPropagation();
        selected = circle;
        status = "editing";
    }

    function handleRightClick(circle: Circle, e: MouseEvent) {
        e.preventDefault();
        snapshot();
        selected = circle;
        status = "editing";
    }

    function handleSizeChange() {
        snapshot();
        status = "drawing";
    }

    function deselect() {
        selected = null;
        status = "drawing";
    }

    function handleKeydown(e: KeyboardEvent) {
        if (e.key === "Escape") deselect();
    }
</script>

<!-- svelte-ignore a11y_no_noninteractive_tabindex -->
<!-- svelte-ignore a11y_no_static_element_interactions -->
<div
    class="flex flex-col items-center justify-center min-h-screen bg-white text-gray-800 p-6"
    onclick={deselect}
    onkeydown={handleKeydown}
    tabindex="0"
>
    <h2 class="text-lg font-medium mb-4 text-gray-700">Circle Drawer</h2>

    <div
        class="bg-white p-5 rounded-lg shadow-md w-full max-w-sm space-y-4 border border-gray-200"
    >
        <div class="flex justify-between">
            <button
                onclick={undo}
                disabled={history <= 0}
                class="px-4 py-2 rounded-md bg-gray-100 text-gray-700 border border-gray-300 hover:bg-gray-200 transition disabled:opacity-50"
            >
                Undo
            </button>
            <button
                onclick={redo}
                disabled={history >= snapshots.length - 1}
                class="px-4 py-2 rounded-md bg-gray-100 text-gray-700 border border-gray-300 hover:bg-gray-200 transition disabled:opacity-50"
            >
                Redo
            </button>
        </div>

        {#if status === "editing" && selected}
            <div class="space-y-2">
                <p class="text-sm text-gray-500">
                    Adjust diameter of circle at ({selected.cx}, {selected.cy})
                </p>
                <input
                    type="range"
                    bind:value={selected.r}
                    min="10"
                    max="100"
                    onchange={handleSizeChange}
                    class="w-full cursor-pointer accent-gray-600"
                />
            </div>
        {/if}
    </div>

    <div
        class="mt-6 bg-gray-100 rounded-lg shadow-lg p-3 border border-gray-300"
    >
        <!-- svelte-ignore a11y_click_events_have_key_events -->
        <svg
            onclick={drawCircle}
            viewBox="0 0 600 400"
            class="w-[600px] h-[400px] bg-white rounded-lg"
        >
            {#each circles as circle}
                <circle
                    {...circle}
                    fill={selected && selected.id === circle.id
                        ? "hsl(210, 80%, 80%)"
                        : "transparent"}
                    stroke="hsl(210, 50%, 40%)"
                    stroke-width="2"
                    class="cursor-pointer transition-all duration-200 hover:fill-gray-300"
                    onclick={(e) => handleSelect(circle, e)}
                    oncontextmenu={(e) => handleRightClick(circle, e)}
                />
            {/each}
        </svg>
    </div>
</div>
