<script>
import{ onMount } from 'svelte';
import '../node_modules/materialize-css/dist/css/materialize.min.css';

import M from 'materialize-css';

onMount(() => {
	M.AutoInit();
	M.Modal.init(document.getElementById("myModal"));
});

let order = {
    drink: "",
    size: "",
    milkType: "",
    syrup: "",
    custom: "",
	temperature: "",
	whippedCream: "",
  };

  let errorMessage = "";
  let result = "";

  const sizes = ["Demi", "Short", "Grande", "Venti", "Trenta"];
  const milkTypes = ["Whole Milk", 
  		"Non Fat", "2% Milk", 
  		"Soy Milk", "Almond Milk", 
		"Coconut Milk", 
		"Breve (half & half)",
		"Oat Milk","Heavy cream",
		"Vanilla, sweet cream"];
  const syrups = ["Vanilla", "Caramel", 
  	"Hazelnut", "Chestnut praline", 
  	"Almond", "Cinnamon Dolce",
	"Peppermint", "Raspberry", "toasted vanilla",
	"Toffee nut","Sugar-free vanilla",
	"Apple brown sugar","Cinnamon dolce",
	"Brown sugar",
	"Honey Ginger"];

	const temperatures = ["Hot", "Iced", "Blended"];
  
	const temperatureString = order.temperature !== 'Hot' ? `${order.temperature} ` : '';
	const whippedCreamString = order.whippedCream ? ' with Whipped Cream' : '';

	const submitOrder = () => {

		if (order.drink == "") {
			errorMessage = "Drink is required";
		} else {
			M.Modal.getInstance(document.getElementById('myModal')).open();
			result = `Your order is ${temperatureString} ${order.drink} ${order.size} ${order.milkType} milk, with ${order.syrup} syrup, ${whippedCreamString} and ${order.custom}`;
		}
  };


</script>

<div class="container" style="margin-top: 100px;">
	<div class="row">
	  <div class="col s12">
		<div class="card">
		  <div class="card-content">
			<span class="card-title">
			  <h5 class="center">Starbucks Order Generator</h5>
			</span>
			<form on:submit|preventDefault={submitOrder} class="container">
			  <div class="row">
				<div class="input-field col s12">
				  <input bind:value={order.drink} type="text" id="drink">
				  <label for="drink">Drink</label>
				  {#if errorMessage}
					<span class="red-text">{ errorMessage }</span>
				  {/if}
				</div>
			  </div>
			  <div class="row">
				<div class="input-field col s6">
				  <select bind:value={order.size}>
					<option value="" disabled selected></option>
					{#each sizes as size}
					  <option value={size}>{size}</option>
					{/each}
				  </select>
				  <label for="size">Size</label>
				</div>
				<div class="input-field col s6">
				  <select bind:value={order.milkType}>
					<option value="" disabled selected></option>
					{#each milkTypes as milkType}
					  <option value={milkType}>{milkType}</option>
					{/each}
				  </select>
				  <label for="milkType">Milk Type</label>
				</div>
				<div class="input-field col s6">
				  <select bind:value={order.syrup}>
					<option value="" disabled selected></option>
					{#each syrups as syrup}
					  <option value={syrup}>{syrup}</option>
					{/each}
				  </select>
				  <label for="syrup">Syrup</label>
				</div>
				<div class="input-field col s6">
					<select bind:value={order.temperature}>
					  {#each temperatures as temp}
						<option value={temp}>{temp}</option>
					  {/each}
					</select>
					<label for="temperature">Temperature</label>
				</div>
				<div class="input-field col s6">
					<p>
					  <label>
						<input type="checkbox" bind:checked={order.whippedCream} />
						<span>Add Whipped Cream</span>
					  </label>
					</p>
				</div>
			  </div>
			  <div class="row">
				<div class="input-field col12">
				  <textarea bind:value={order.custom} class="materialize-textarea" name="custom" id="custom" cols="30" rows="10"></textarea>
				  <label for="custom">Add Additional Ingredients</label>
				</div>
			  </div>
			  <button type="submit" class="btn waves-effect waves-light">Submit</button>
			</form>
		  </div>
		</div>
	  </div>
	</div>
  </div>

  <div id="myModal" class="modal">
	<div class="modal-content">
	  <h4>Your Order is here</h4>
	  <p class="center">{ result }</p>
	</div>
	<div class="modal-footer">
	  <a href="#!" class="modal-close waves-effect waves-green btn-flat">Close</a>
	</div>
  </div>