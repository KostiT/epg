<template>
	<div class="timeline">
		<div class="timeline-icon">
			<i class="fa fa-star fa-2x" aria-hidden="true"></i>
		</div>
		<div class="timeline-body">
			<div v-for="entry in entries" :class="entry.date == '14.04.' ? 'active' : ''" :key="entry.id">
				<h5>{{ entry.title }}</h5>
				<h6>{{ entry.date }}</h6>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				entries: [
					{title: 'Mon', date: '12.04.'},
					{title: 'Tue', date: '13.04.'},
					{title: 'Wed', date: '14.04.'},
					{title: 'Thu', date: '15.04.'},
					{title: 'Fri', date: '16.04.'},
				]
			}
		}
	};
</script>

<style scoped>
	.timeline {
		background-color: #202020;
		border-bottom: 1px solid #545454;
		display: grid;
		grid-template-columns: 100px auto;
	}

	.timeline-icon {
		display: flex;
		width: 100px;
		height: 80px;
		color: #545454;
		align-items: center;
		justify-content: center;
		box-shadow: 6px 0px 20px -5px rgba(0, 0, 0, 0.8);
	}

	.timeline-body { overflow-x: scroll; overflow-y: hidden; white-space: nowrap; }
	.timeline-body div { display: inline-block; width: 100px; text-align: center; color: #545454; }
	.timeline-body div.active { color: #fff; }
	.timeline-body div h5 { margin-bottom: 5px; }
	.timeline-body div h6 { margin: 0; }
</style>