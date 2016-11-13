<template>
	<div class="hello">
		<h1>{{ msg }}</h1>
		<button @click='onclickMe'>open mouse</button>
	</div>
</template>

<script>
	export default {
		data () {
			return {
				msg: '子组件传给父组件了！'
			}
		},
		props:['msgfromfather'],
		methods:{
			onclickMe:function(){
				console.log(this.msgfromfather);
				this.$emit('child-tell',this.msg);
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	h1, h2 {
		font-weight: normal;
	}

	ul {
		list-style-type: none;
		padding: 0;
	}

	li {
		display: inline-block;
		margin: 0 10px;
	}

	a {
		color: #42b983;
	}
</style>
