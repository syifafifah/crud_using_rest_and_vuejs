<template>
	<div>
		<div class="row">
			<div class="col-md-12">
				<div class="card" style="margin-top:20px;">

					<div class="card-header text-white mb-3 bg-dark">
						<div class="row">
							<div class="col-md-10">
								<h4>Menus</h4>
							</div>
							<div class="col-md-2">
								<router-link class="btn btn-primary btn-sm" to="/create">+ Add new menu</router-link>
							</div>
						</div>
					</div>

					<div class="card-body">
						<table class="table table-bordered">
							<thead>
								<tr>
									<th scope="col">Name</th>
									<th scope="col">Description</th>
									<th scope="col">Category</th>
									<th scope="col">Prize</th>
									<th scope="col">Action</th>
								</tr>
							</thead>
							<tbody>
								<tr v-for="(menu, id) in menus.data" v-bind:key="id">
									<td>{{menu.name}}</td>
									<td>{{menu.desc}}</td>
									<td>{{menu.category}}</td>
									<td>{{menu.prize}}</td>
									<td>
										<div class="btn-group btn-group-sm" role="group" aria-label="">
											<router-link class="btn btn-dark btn-sm" :to="'/detail/'+menu.id">Edit</router-link>
											<button class="btn btn-warning btn-sm" v-on:click="deleteData(menu.id)" :title="menu.id">Delete</button>
										</div>
									</td>
								</tr>
							</tbody>
						</table>
					</div>
				</div>

			</div>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				// variabel penamping hasil fetch dari API
				menus: []
			};
		},
		created() {
			this.loadData();
		},
		methods: {
			loadData() {
				axios.get("http://localhost:8000/menus").then(response => {
					this.menus = response.data;
				});
			},
			deleteData(id) {
				axios.post("http://localhost:8000/menus/delete/" + id).then(response => {
					alert('Deleting menu success.');
					this.loadData();
				});
			}
		}
	};
</script>