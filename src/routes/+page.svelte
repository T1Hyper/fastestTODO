<script>
    let todo2 = $state("");
    let todolist = $state(
    (() =>  {
    try {
        return JSON.parse(localStorage.getItem("todolist") ?? "[]");
        } catch {
                return [];
                }
            })()
    );

$effect(() => {
  localStorage.setItem("todolist", JSON.stringify(todolist));
});

    function pusher() {
        if (todo2 !== "") {
            todolist.push({
                text: todo2,
                completed: false,
                type: "ostatní",
            });
            todo2 = "";
        }
    }
    function RemoveTODO() {
        if(confirm("Chceš všechno zrušit?")){
            todolist.splice(0, todolist.length)
        }
    }
    function RemoveTODO2(index) {
        todolist.splice(index, 1);
    }
</script>

<div class="py-4 bg-blue-400">
    <div class="item-center flex flex-row">
        <p class="pl-5 text-5xl font-bold text-white font-impact">TODO LIST</p>
        <div class="flex flex-1 justify-center gap-5">   
            <input
                class="bg-black border-3 rounded-xl text-white placeholder:text-white p-1"
                type="text"
                bind:value={todo2}
                onkeydown={(e) => e.key === "Enter" && pusher()}
                placeholder="Zadej Úkol"/>
            <button class="border-3 rounded-2xl bg-green-400 p-1" onclick={pusher}
                >Přidat</button>
            <button class="border-3 rounded-2xl bg-red-400 p-1" onclick={RemoveTODO}
                >Smazat vše</button>
        </div>
    </div>
</div>
<div class="pozadi">
<div class="flex">
<div class="">
<div class="px-5 pt-20 pb-150 border-5 m-10 rounded-4xl max-w-130 min-w-130 bg-blue-900">
    <p class="text-center text-black text-5xl">Počet úkolů: {todolist.length-(todolist.filter(i => i.completed).length)}</p>
    <p class="text-center text-3xl text-green-300 mt-16">Splněno úkolů: {todolist.filter(i => i.completed).length}</p>
    <p class="text-center text-white text-3xl mt-6">Celkem: {todolist.length}</p>
    <div class="flex flex-row justify-center gap-9">
        <p class=" text-purple-400 text-3xl mt-6">Prace: {todolist.filter(i => i.type==="work").length}</p>
        <p class=" text-white text-3xl mt-6">Ostatní: {todolist.filter(i => i.type==="ostatni").length}</p>
        <p class=" text-yellow-400 text-3xl mt-6">Osobní: {todolist.filter(i => i.type==="personal").length}</p>
    </div>
</div>
</div>
    <div class="text-center">
        <ul class="inline-block mt-3">
            {#each todolist as item, index}
                <div
                    class="flex items-center text-white text-center divide-y-5 pl-10 font-sans"
                >
                    <button
                        class="border-2 rounded py-1 mr-5 px-2 bg-green-800 text-green-300 hover:text-black"
                        onclick={() => {
                            item.completed = !item.completed;
                        }}>Hotovo</button>
                    <li
                        class={[
                            "pt-5.5 pb-1.5 px-5 text-2xl text-center flex-1 mb-5",
                            item.completed
                                ? " text-green-500"
                                : " "]}>
                                <input class="min-w-150 max-w-150" type="text" bind:value={item.text} placeholder="{item.text}"></li>
                    <li class={["pt-5.5 pb-1.5 px-0 text-2xl text-center flex-1 mb-5 min-w-25 max-w-25 text-gray-400",
                                        item.type === "práce" &&
                                          "text-purple-400",
                                        item.type === "osobní" &&
                                          "text-yellow-400"]}
                    >[{item.type}]</li>
                    
                    <button
                        class="min-w-20 max-w-20 border-2 rounded-2xl py-1 ml-5 px-2 bg-purple-800 text-purple-300 hover:text-black"
                        onclick={() => {
                            item.type = "práce";
                        }}>Práce</button
                    >
                    <button
                        class="min-w-20 max-w-20 border-2 rounded-2xl py-1 ml-2 px-2 bg-gray-800 text-gray-300 hover:text-black"
                        onclick={() => {
                            item.type = "ostatní";
                        }}>Ostatní</button
                    >
                    <button
                        class="min-w-20 max-w-20 border-2 rounded-2xl py-1 ml-2 px-2 bg-yellow-800 text-yellow-300 hover:text-black"
                        onclick={() => {
                            item.type = "osobní";
                        }}>Osobní</button
                    >
                    <button
                        class="border-2 rounded py-1 ml-10 px-2 bg-red-800 text-red-200 hover:text-black"
                        onclick={() => RemoveTODO2(index)}>Smazat</button
                    >
                </div>
            {/each}
        </ul>
    </div>
</div>
</div>

<style>
    .pozadi {
        background-color: rgb(10, 17, 77);
        min-height: 100vh;
        font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
    }
</style>
