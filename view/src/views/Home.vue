<template>
	<section>
		<article v-for="item in $store.state.accounts" :key="item.screenName">
			<img @click="open(item.screenName)" :src="`https://res.cloudinary.com/narusejun/image/twitter_name/h_200/${item.screenName}.jpg`">
			<div class="content">
				<h2 @click="open(item.screenName)">{{ item.name }}</h2>
				<h3 @click="open(item.screenName)">@{{ item.screenName }}</h3>
				<p>{{ item.bio }}</p>
			</div>
			<div class="action" @click="reply(item.screenName)">クソリプ</div>
		</article>
	</section>
</template>

<style scoped lang="scss">
section {
	display: flex;
	flex-wrap: wrap;
}
article {
	box-shadow: 0 2px 3px rgba(10,10,10,.1), 0 0 0 1px rgba(10,10,10,.1);
	margin: 1em 1em 0 0;
	display: flex;
	flex-direction: column;

	$radius: 4px;
	border-radius: $radius;

	$card-size: 200px;
	width: $card-size;

	img {
		cursor: pointer;
		flex: 0 0 auto;
		border-radius: $radius $radius 0 0;
		width: $card-size;
		height: $card-size;
	}
	.content {
		flex: 1 0 auto;
		padding: 1.2em;
		word-wrap: break-word;

		h2 {
			cursor: pointer;
			margin: 0;
			font-weight: 400;
			line-height: 1.1em;
			color: #444;
		}
		h3 {
			cursor: pointer;
			margin: 0;
			font-weight: 400;
			line-height: 1.1em;
			font-size: .8em;
			color: #888;
		}
		p {
			line-height: 1.1em;
			font-size: .9em;
			color: #666;
		}
	}
	.action {
		flex: 0 0 auto;
		color: #9880ff;
		border-top: 1px solid #EEE;
		text-align: center;
		padding: .6em;
		cursor: pointer;
		transition: 100ms all;

		&:hover {
			background-color: #EEE;
		}
	}
}
</style>

<script>
export default {
	computed: {
		replies() {
			const replies = this.$store.state.replies.filter(r => r.enabled);
			return replies.length ? replies : this.$store.state.replies;
		},
	},
	methods: {
		open(name) {
			window.open(`https://twitter.com/${name}`);
		},
		reply(name) {
			const replies = this.replies;
			const {text} = replies[parseInt(replies.length * Math.random())];
			window.open(`https://twitter.com/intent/tweet?text=${encodeURIComponent(text.replace(/{{@}}/g, `@${name}`).trim().substr(0, 140))}`);
		},
	}
}
</script>
