<script>

let {id = "#id"} = $props()

let count = $state(0); //$state variabile reattiva. IMPORTANTE perchè quando il valore cambia, Svelte aggiornerà automaticamente tutti i punti dell'interfaccia che utilizzano questa variabile

function increment() {
  count += 1;
}

let double =$derived(count * 2) //lo stato di double dipende dallo stato di count. Non posso usare $derived senza uno $state. Ogni volta che count cambia, double verrà ricalcolato automaticamente


let array = $state([1,2,3,4,5]); //viene utilizzato $state per rendere l'array modificabile
let sum = $derived(array.reduce((a, b) => a + b, 0));

function addNumber() {
  array.push(array.length + 1)
}

$inspect(array) //$inspect permette di monitorare i cambiamenti di una variabile reattiva che si vede nella console del browser

//$effect((() => {alert(`Il valore del contatore è ${count}`)}));
</script>

<div>
<h1>Sono il Componente {id}</h1>
<div class = subComponente>
<button onclick = {increment}>Clicked {count}</button>
<p>Il doppio di {count} è {double}</p>
</div>
<div class = subComponente>
<button onclick = {addNumber}>Add number</button>
<p>{array.join(" + ")} = {sum}</p> <!--con join unisci gli elementi dell'array con +-->
</div>
</div>

<style>
	h1 {
		color: blue;
	}
	button {
		background-color: yellow;
	}
  div {
		border: 1px solid black;
    padding: 10px;
    width: 300px;
    text-align: center;
    align-items: center;
    border-radius: 10px;
	}

  .subComponente {
    background-color: lightblue;
    padding: 10px;
    width: 200px;
    border-radius: 10px;
    margin: 10px auto;
	}
</style>