<template>
	<div>
		<p>
			<nuxt-link v-if="page" :to="'/?page=' + page">Back to home page</nuxt-link>
			<nuxt-link v-else to="/">Back to home page</nuxt-link>
		</p>

		<img :src="user.avatar">

		<ul>
			<li>
				{{ user.id }}
			</li>
			<li>
				{{ user.first_name }}
			</li>
			<li>
				{{ user.last_name }}
			</li>
		</ul>
	</div>
</template>

<script type="text/javascript">

	import axios from 'axios'
	
	export default {

		async asyncData( { params } ) {

			const { data } = await axios.get( `https://reqres.in/api/users/${ params.id }` )

			return {
				page: params.page ? params.page : '',
				user: data.data
			}

		},

		mounted() {

			// console.log( $nuxt.$route.redirectedFrom )

		}

	}

</script>