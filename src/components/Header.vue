<template>
	<div class="navbar">
		<a href="#">
			<i class="fa fa-user"></i>
		</a>

		<a href="#" class="logo">
			<img src="../assets/logo.png" alt="logo">
		</a>

		<a href="#">
			<i class="fa fa-search"></i>
		</a>
	</div>
</template>

<script>
	export default {

	};
</script>

<style scoped>
  .logo {
    display: block;
    height: 40px;
  }

	.navbar {
		top: 0;
		z-index: 5;
		display: grid;
		padding: 10px 0;
		position: sticky;
		text-align: center;
		align-items: center;
		background-color: #000;
		position: -webkit-sticky;
		grid-template-columns: 15% auto 15%;
	}

	.navbar a { display: block; color: #fff; }
	.navbar a i { font-size: 25px; }
</style>
