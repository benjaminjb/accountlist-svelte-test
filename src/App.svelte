<script>
	const fetchAccounts = (async () => {
		const response = await fetch(__myapp.env.DBASVCSAPI_URL + "/accounts/");

		const data = await response.json()
		return data
	})()
</script>

{#await fetchAccounts}
	<p>...waiting</p>
{:then data}
	<table>
		<thead>
		<tr>
			<th>Account ID</th>
			<th>Account Name</th>
			<th>Account Number</th>
			<th>Account Type</th>
		</tr>
		</thead>
		<tbody>
		{#each data as account, index}
			<tr key={index}>
			<td>{account.id}</td>
			<td>{account.name}</td>
			<td>{account.number}</td>
			<td>{account.type}</td>
			</tr>
		{/each}
		</tbody>
	</table>
{:catch error}
	<p>An error occurred! {error}</p>
{/await}