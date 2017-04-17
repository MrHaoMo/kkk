<style type="text/css">
	body {
		 font-family: Helvetica Neue, Arial, sans-serif;
		 font-size: 14px;
		 color: #444;
		}
				 
				table {
				 border: 2px solid #42b983;
				 border-radius: 3px;
				 background-color: #fff;
				}
			th {
			 background-color: #42b983;
			 color: rgba(255,255,255,0.66);
			 cursor: pointer;
			 -webkit-user-select: none;
			 -moz-user-select: none;
			 -user-select: none;
			}
			 
			td {
			 background-color: #f9f9f9;
			}
			 
			th, td {
			 min-width: 120px;
			 padding: 10px 20px;
			}
</style>
<template>			
	
	<div id="app">
			<div class="dropdown">
		        <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown" aria-haspopup="true" aria-expanded="true">
		         {{title}}
		        <span class="caret"></span>
		         </button>
		      <ul class="dropdown-menu" aria-labelledby="dropdownMenu1">
			    <li v-for="item in content"><a href="#" @click='dian'>{{item.name}}</a></li>	    	    	    
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
	head:['name','power','dates','mark'],
	content:
		[
		{name:'zs',power:'20',dates:69,mark:490},
		{name:'rzs',power:'210',dates:769,mark:740},
		{name:'zts',power:'240',dates:649,mark:420}
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
