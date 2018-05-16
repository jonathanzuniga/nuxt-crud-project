<template>
	<div>
		<table>
			<tbody>
				<tr v-for="user in users" :key="user.id">
					<td>
						<img :src="user.avatar">
					</td>

					<td>
						<span>{{ user.first_name }} {{ user.last_name }}</span>
					</td>

					<td>
						<nuxt-link :to="{ name: 'edit-id', params: { id: user.id, page: page } }">Edit</nuxt-link>
					</td>
				</tr>
			</tbody>
		</table>

		<nuxt-link v-if="page > 1" :to="'?page=' + ( page - 1 )">&lt; Prev</nuxt-link>
		<a v-else class="disabled">&lt; Prev</a>

		<span>{{ page }} / {{ totalPages }}</span>

		<nuxt-link v-if="page < totalPages" :to="'?page=' + ( page + 1 )">Next &gt;</nuxt-link>
		<a v-else class="disabled">Next &gt;</a>
	</div>
</template>

<script type="text/javascript">
	
	import axios from 'axios'

	export default {

		watchQuery: [ 'page' ],

		async asyncData( { query } ) {

			const page =+ query.page || 1
			const per_page = 5
			const { data } = await axios.get( `https://reqres.in/api/users?page=${ page }&per_page=${ per_page }` )

			return {
				page: +data.page,
				totalPages: data.total_pages,
				users: data.data
			}

		},

		key: to => to.fullPath

	}

</script>