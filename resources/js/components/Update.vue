<template>
	<div class="row">
		<div class="col-md-3"><br></div>
		<div class="col-md-6">
			<div class="card" style="margin-top:20px;">

				<div class="card-header text-white mb-3 bg-dark">
					Edit menu
				</div>

				<div class="card-body">
					<form @submit.prevent="updateData()">
						<div class="form-group">
							<label>Menu name</label>
							<input type="text" class="form-control" v-model="form.name" required>
						</div>
						<div class="form-group">
							<label>Description</label>
							<input type="text" class="form-control" v-model="form.desc" required>
						</div>
						<div class="form-group">
							<label>Category</label>
							<input type="text" class="form-control" v-model="form.category" required>
						</div>
						<div class="form-group">
							<label>Price</label>
							<input type="number" class="form-control" v-model="form.prize" required style="width:150px;-moz-appearance:textfield;input::-webkit-outer-spin-button,input::-webkit-inner-spin-button{-webkit-appearance: none; margin: 0;}">
						</div>
						<button class="btn btn-primary">Submit</button>
						<router-link to = "/"><button class="btn btn-dark">Back</button></router-link>
					</form>
				</div>

			</div>
		</div>
		<div class="col-md-3"><br></div>
	</div>
</template>

<script>
    export default {
        data() {
        	return {
        		form: {
        			name: '',
        			desc: '',
        			category: '',
        			prize: ''
        		}, 
        		menus: []
        	};
        },
        created() {
        	this.loadData();
        },
        methods: {
        	loadData() {
        		axios.get("http://localhost:8000/menus/" + this.$route.params.id).then(response => {
        			this.menus = response.data;

        			this.form.name = this.menus.data[0].name;
        			this.form.desc = this.menus.data[0].desc;
        			this.form.category = this.menus.data[0].category;
        			this.form.prize = this.menus.data[0].prize;       		
        		});
        	},
        	updateData() {
        		axios.post("http://localhost:8000/menus/update/" + this.$route.params.id, {
        			name: this.form.name,
        			desc: this.form.desc,
        			category: this.form.category,
        			prize: this.form.prize
        		}).then(response => {
        			// go to menu list view
        			this.$router.push('/');
        		});
        	}
        }
    };
</script>