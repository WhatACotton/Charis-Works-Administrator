<script>
	const user = localStorage.getItem('role');
	if (user === 'Seller' || user === 'admin') {
	} else {
		location.href = '/';
	}
	console.log(user);
</script>

<h1>About</h1>
