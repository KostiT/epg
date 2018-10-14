<template>
	<div class="footer">
		<a href="#"><i class="fa fa-home"></i></a>
		<a href="#"><i class="fa fa-youtube-play"></i></a>
		<a href="#" class="active"><i class="fa fa-th-list"></i></a>
		<a href="#"><i class="fa fa-undo"></i></a>
		<a href="#"><i class="fa fa-bookmark"></i></a>
	</div>
</template>
<script>
	export default {

	};
</script>

<style>
	.footer {
		bottom: 0;
		z-index: 5;
		display: grid;
		padding: 10px 0;
		position: sticky;
		text-align: center;
		align-items: center;
		background-color: #000;
		position: -webkit-sticky;
		grid-template-columns: repeat(5, auto);
	}

	.footer a {
		color: #fff;
		font-size: 26px;
	}

	.footer a.active { color: #e1a21e; }
</style>