<script>
	const videos = [
		{ url: 'https://www.youtube.com/watch?v=S4bn6gg-BmE', name: 'Messi' },
		{ url: 'https://www.youtube.com/watch?v=MD6WXsjdcsY', name: 'Ronaldo' },
		{ url: 'https://www.youtube.com/watch?v=yTGr45ZQRdA', name: 'Neymar' }
	];
</script>

<div>
	<h5>Famous soccer players:</h5>
	<ul>
		{#each videos as video}
			<li>{video.name} <a href={video.url}> {video.url}</a> </li>
		{/each}
	</ul>
</div>
