<script>
	let link = ""

	let responseOfSend = null

	async function makeReq() {
		let response = await fetch("http://localhost:8000/", {
			method: 'POST',
			headers: {
				'Accept': 'application/json',
				'Content-type': 'application/json'
			},
			body: JSON.stringify({
				url: link
			})
		})
		responseOfSend = await response.json()
	}
</script>

<div class="divStyle">
	<h1>Rick Roll Detector</h1>
	<p>Is your friend being sus!?!? Enter the link to check if it's a rick roll.</p>
	<input class="inputStyle" placeholder="Enter link here" bind:value={link}/>
	<button class="buttonStyle" on:click={makeReq}>Check</button>
	{#if responseOfSend == null}	
		<p></p>
	{:else if responseOfSend.Result == "[!] The link is a Rick Roll. Do not open it unless u actually like rick astley which is VERY RARE"}
		<p style="color: orange;">{responseOfSend.Result}</p>
	{:else if responseOfSend.Result == "[+] The link IS NOT a Rick Roll. You can safely open it in your browser"}
		<p style="color: green;">{responseOfSend.Result}</p>
	{:else} 
		<p style="color: red;">{responseOfSend.Result}</p>
	{/if}

</div>

<style>
	.divStyle {
		display: flex;
		flex-direction: column;
		height: 100vh;
		width: 100%;
		justify-content: center;
		align-items: center;
	}
	.inputStyle {
		width: 750px;
		border-radius: 5px;
		background-color: transparent;
	}
	.buttonStyle {
		background-color: limegreen;
		color: black;
		width: 100px;
		height: 50px;
		font-size: 20px;
		border-radius: 5px;
		border: 0px solid transparent;
	}
	@media (prefers-color-scheme: dark) {
		:root {
			background-color: rgb(36, 36, 36);
		}
		p {
			color: white;
		}
		h1 {
			color: white;
		}
		input {
			color: white;
		}
	}
</style>