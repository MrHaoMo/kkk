<template>
	<div id="app">
		
		<input :value="values" :type="types" v-if="types == 'text'" @keyup.enter="onEnter"/>
	    <select class="form-control" :value="values"  :type="types" v-if="types == 'select'">	    
         <option v-for="item in items">{{item}}</option>
        </select>
        <!--<input class="form-control" :value="value" :type="types" v-if="types == 'textarea'"></input>
	   <input class="form-control" :value="value" :type="types" v-if="types == 'number'"></input>
	   <input class="form-control" :value="value" :type="types" v-if="types == 'date'"></input>
	   <input class="form-control" :value="value" :type="types" v-if="types == 'checkbox'"></input>
	   <input class="form-control" :value="value" :type="types" v-if="types == 'radio'"></input>	-->
	   <tabs></tabs>
		
	</div>
	
</template>


<script>
import tabs from './tabs'
export default {
	components:{
		tabs
	},
  props: {
    value: String,
    type: {
      type: String,
      validator: function (value) {
        console.log('value:', value)
        return ['text', 'textarea', 'select', 'number', 'date', 'checkbox', 'radio'].indexOf(value) >= 0
      },
      default: function () {
        return 'textarea'
      }
    },
    options: Array,
    onEnter: {
      type: Function,
      default () {
      	console.log('gggggggg')
      }
    }
  },
  data () {
    return {
      types: 'text',
        values:'',
        items:['fhdk','fklg','flkf']
    }
  },
  computed: {
  }
}
</script>
