<style type="text/css">
	@import '../assets/css/bootstrap.min.css'
	@import '../assets/css/bootstrap-table.min.css'
</style>
<template>			
	
	<div id="app">
			<div class="dropdown">
		        <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu2" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
		         {{title}}
		        <span class="caret"></span>
		         </button>
		      <ul class="dropdown-menu" aria-labelledby="dropdownMenu2">
			    <li v-for="item in content"><a href="#" @click='dian'>{{item.names}}</a></li>	    	    	    
			  </ul>
			 </div>
			<form id="search">
				<input type="text" v-model="values" v-show="showall"/>
			</form>			
			<table class="table table-borderd" :valuett='values'
				:contents='content'
				:heads='head'
				 v-show="isshow">
			<thead>
			<tr>
				<th v-for="item in head">{{item}}</th>					
			</tr>
			</thead>
			<tbody>
				<tr v-for="key in content
					       | filterBy values">
				<td v-for="item in head">{{key[item]}}</td>
				
			   </tr>
			</tbody>				
		</table>
		</div>
</template>

<script>

	export default{
		props: {
   valuett:String,
   contents:Array,
   heads:Array 
  },
   data () {
   	return {
   	values:'',
	isshow:false,
	showall:false,
	title:'zs',
	head:['names','power','dates','mark'],
	content:
		[
		{names:'zs',power:'20',dates:69,mark:490},
		{names:'rzs',power:'210',dates:769,mark:740},
		{names:'zts',power:'240',dates:649,mark:420}
		]	
   	}	
    },
    watch: {
	'values': function() {
		this.isshow =true
		console.log(this.isshow)
		}
	},
	methods: {
	'dian': function(){
		this.showall =true }
}
	}
</script>
