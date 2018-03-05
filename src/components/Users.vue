<template>
	<div class="users">
		<h1>users</h1>
		<!-- 添加用户信息 -->
		<form @submit="handleAddUser">
			<input type="text" v-model="newUser.name" placeholder="Enter name">
			<input type="email" v-model="newUser.email" placeholder="Enter email">
			<input type="submit"  value="Submit" name="">
		</form>

		<ul>
			<li v-for="user in users">
				<input type="checkbox" v-model="user.contacted" name="">
				<span :class="{contacted:user.contacted}">
					{{user.name}} :{{user.email}}
				     <button @click="handleDeleteUser(user)">X</button>
				</span>
				

			</li>
		</ul>
	</div>
</template>
<script type="text/javascript">
	export default{
	   name:'users',
	   data(){
	        return{
               users:[],
               newUser:{}
	        }
	    },
	    methods:{
	        handleAddUser:function(e){
             e.preventDefault();
	         this.users.push({
	           name:this.newUser.name,
	           email:this.newUser.email,
	           contacted:false
	           })
	         },
	        handleDeleteUser(user){
              this.users.splice(this.users.indexOf(user),1)
	        }
	    },
	    created:function(){
          this.$http.get('http://jsonplaceholder.typicode.com/users').then(function(response){
             this.users=response.data;
      })
	    }
    }
</script>
<style type="text/css" scoped="scoped">
	.contacted{
	text-decoration:line-through;
}
</style>