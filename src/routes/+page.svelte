<script lang="ts">
	let user = '';
	export const GetCustomer = async () => {
		try {
			const response = await fetch('http://' + 'localhost' + ':80/go/GetCustomer', {
				method: 'GET',
				mode: 'cors',
				headers: {
					'Content-Type': 'application/json'
				},
				credentials: 'include'
			});
			const json = await response.json();

			if (response.status === 401) {
				localStorage.setItem('IsRegistered', 'false');
			}

			user = json.Customer.role;
			//出品者
			if (user === 'Seller') {
				localStorage.setItem('role', 'Seller');
			//管理者
			} else if (user === 'Admin') {
				localStorage.setItem('role', 'Admin');
			}
		} catch (error) {
			console.log(error);
		}
	};
	if (user === '') {
		GetCustomer();
	}
</script>

<p>{user}</p>
{#if user === 'Seller'}
	<ul>
		<li>ようこそ出品者様</li>
	</ul>
{:else if user === 'Admin'}
	<ul>
		<li>管理者ですね</li>
	</ul>
{:else if user}
	<ul>
		<li>ここに来るべきではなかった。ここには何もない...</li>
	</ul>
{:else}
	<ul>
		<li>ログインしてください</li>
	</ul>
{/if}
