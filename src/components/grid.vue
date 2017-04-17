<style type="text/css">
  .edit-grid {
    max-height:500px;
    overflow:auto;
  }
</style>
<template>
	<div class="tatal">
		<div class="container"> 
		<table class="table table-hover">
    <thead>
      <tr>
        <th v-if="isShowAction"><input type="checkbox" value="true" v-model="isSelectedAll" />&nbsp;</th>
        <th v-for="item in grides"
          :class="{active: sortitem === item.name}">
          <a href="#">{{item.name | capitalize}}
            <span class="caret" v-show="sortOrders[item.name] < 0"></span>
          </a>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="entry in gridData">
        <td v-if="isShowAction"><input type="checkbox" true-value="true" false-value="false" v-model="entry.isChecked" /></td>
        <td v-for="item in grides">
          {{entry[item.name]}}
        </td>
      </tr>
    </tbody>
  </table>
	<div class="form-group" v-if="isShowAction">
     <button class="btn btn-primary" @click="add">Add</button> 
    <button class="btn btn-primary" @click="edit" >Edit</button>
    <button class="btn btn-default" @click="deletes" >Delete</button>
    </div>
	   
    </div>
	<modal :show.sync="showEditModal" effect="fade" width="90%">
		<div slot="modal-header" class="modal-header">
	    <h4 class="modal-title">Edit Selected Records</h4>
	    </div>
	     <div slot="modal-body" class="modal-body edit-grid">
	     	<table class="table table-hover">
		      <thead>
		        <tr>
		          <th>&nbsp;</th>
		          <th v-for="item in grides">{{item.title}}</th>
		        </tr>
		      </thead>
		      <tbody>
		        <tr v-for="entry in gridData
		        	       |filterBy true in 'isChecked'">
		          <td><input name="chkEntry" type="radio" true-value="true" false-value="false" @click="select(entry)" /></td>
		          <td v-for="item in grides">
		           <field :value.sync="entry[item.name]" :type="item.type" :options="item.options"></field>
		          </td>
		        </tr>
		      </tbody>
            </table>
            <fieldset>
		      <legend>Details</legend>
		      <div v-for="item in grides">
                  <label>{{item.title}}</label>
                  <field :value.sync="selectedRow[item.name]" :type="item.type" :options="item.options"></field>
              </div>
           </fieldset>
	     </div>
	     <div slot="modal-footer" class="modal-footer">
	    <button type="button" class="btn btn-default" @click='showEditModal = false'>Cancel</button>
	    <button type="button" class="btn btn-success">Save</button>
	    </div>
	</modal>
	</div>
</template>		
<script type="text/javascript">
import Vue from 'vue'
import field from './filed'
import { modal } from 'vue-strap'
export default {components: {
  field,
  modal},
  props: {
    gridData: Array,
    grides: Array,
    sortitem: String,
    order: String,
    selectedRow: Object,
    onSave: {
      type: Function,
      default: function (items) {
        console.log('grid onSave items:', items)
      }
    },
    isShowAction: {
      type: Boolean,
      default: function () {
        return false
      }
    }
  },
  data () {
    return {
      showEditModal: false,
      sortOrders: {},
      gridData:[{name: 'id', title: 'Id', type: 'number'},
       {name: 'sex', title: 'Sex', type: 'select', options: ['M', 'F']},
        {name: 'menuName', title: 'Menu Name', type: 'text'}
        ],
      grides:[{name: 'id', title: 'Id', type: 'number'},
       {name: 'sex', title: 'Sex', type: 'select', options: ['M', 'F']},
        {name: 'menuName', title: 'Menu Name', type: 'text'}
        ]
    }
  },
  computed: {
  },
  methods: {    
    select: function (entry) {
      this.selectedRow = entry
    },
    edit: function () {
      console.log('edit')
      this.showEditModal = true
    },
    delete: function () {
      console.log('delete')
    },
    add: function () {
      console.log('edit')
    }
  }
}

</script>
