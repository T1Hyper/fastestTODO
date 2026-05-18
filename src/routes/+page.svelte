<style>
@import "tailwindcss";
.cislo{
    color: rgb(255, 255, 255);
    text-decoration: underline;
    text-underline-offset: 1rem;
    font-size: 4rem;
    text-align: center;

}
.zadej{
    text-align: center;
    justify-content: center;
    display: inline-block;
    padding: 1rem 2rem 1rem 2rem;
    border-radius: 15px;
    margin-top: 2.5rem;
}
.pozadi
{
    background-color: rgb(10, 17, 77);
    min-height: 100vh;
    font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
}
</style>
<script>
    let cisloX = $state(0)
    let cisloY = $state(0)
    let vysledek = $state(0)

function zadej(){
    const valueX = $state(prompt("napiš cislo X", cisloX.toString()));
    cisloX = Number(valueX)

    const valueY = $state(prompt("napiš cislo Y", cisloY.toString()));
    cisloY = Number(valueY)

    const inter = prompt("+,-,/,* ?", "+")
    if (inter == "+")
    {
        vysledek = cisloX + cisloY
    }
    else if (inter == "-")
    {
        vysledek = cisloX - cisloY
    }
    else if (inter == "/")
    {
        vysledek = cisloX / cisloY
    }
    else(inter == "*")
    {
        vysledek = cisloX * cisloY
    }
}
    const todolist = $state([]);
function pushni(parametr){
   let todo = prompt("co chceš v todo listu?")
    parametr.push(todo)
}
</script>

<div class="pozadi">
    
    <div style="justify-content: center; display: flex">
        <button class="border-5 rounded-full py-1.5 px-5 mt-9 bg-white" onclick={zadej}>zadej</button>
    </div>
    <h1 class="bg-blue-550 text-white text-center mt-6 text-5xl">výpočet je: {vysledek}</h1>
    
    <div style="justify-content: center; display: flex">
        <button class="border-5 rounded-full py-1.5 px-5 mt-22 bg-white" onclick={() => pushni(todolist)}>přidej do TODO listu</button>
    </div>
    <style>
        .ulko{
            color: white;
        }
    </style>
    <div class="text-center">
        <ul class="inline-block border-collapse text-white text-center divide-y-5">
            {#each todolist as item}
            <li class="py-1.5 px-5 text-xl text-center">{item}</li>
            {/each}
        </ul>

    </div>
</div>
