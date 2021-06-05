<template>
	<div class="post-preview">
		<div class="container quillWrapper">
			<h2>{{ this.currentBlog[0].blogTitle }}</h2>
			<h4>
				Posted on:
				{{ new Date(this.currentBlog[0].blogDate).toLocaleString("en-us", { dataStyle: "long" }) }}
			</h4>
			<div class="image-wrap">
				<img :src="this.currentBlog[0].blogCoverPhoto" alt="" />
			</div>
			<div class="post-content ql-editor" v-html="this.currentBlog[0].blogHTML"></div>
		</div>
	</div>
</template>

<script>
export default {
	name: "viewBlog",
	data() {
		return {
			currentBlog: null,
		};
	},
	async mounted() {
		this.currentBlog = await this.$store.state.blogPosts.filter((post) => {
			return post.blogID === this.$route.params.blogid;
		});
		console.log(this);
	},
};
</script>


<style lang="scss">
.post-preview {
	h4 {
		font-weight: 400;
		font-size: 14px;
		margin-bottom: 24px;
	}

	img {
		height: 500px;
		object-fit: cover;
	}
}
</style>