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
        <th v-for="key in columns"
          @click="sortBy(key.name)"
          :class="{active: sortKey === key.name}">
          <a href="#">{{key.name}}
            <span class="caret" v-show="sortOrders[key.name] < 0"></span>
          </a>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="entry in gridData">
        <td v-if="isShowAction"><input type="checkbox" true-value="true" false-value="false" v-model="entry.isChecked" /></td>
        <td v-for="key in columns">
          {{entry[key.name]}}
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
		          <th v-for="key in columns">{{key.title}}</th>
		        </tr>
		      </thead>
		      <tbody>
		        <tr v-for="entry in gridData
		        	       |filterBy true in 'isChecked'">
		          <td><input type="radio" true-value="true" false-value="false" @click="select(entry)" /></td>
		          <td v-for="key in columns">
		           <field :value.sync="entry[key.name]" :type="key.type" :options="key.options"></field>
		          </td>
		        </tr>
		      </tbody>
            </table>
            <fieldset>
		      <legend>Details</legend>
		      <div v-for="key in columns">
                  <label>{{key.title}}</label>
                  <field :value.sync="selectedRow[key.name]" :type="key.type" :options="key.options"></field>
              </div>
           </fieldset>
	     </div>
	     <div slot="modal-footer" class="modal-footer">
	    <button type="button" class="btn btn-default" @click='showEditModal = false'>Cancel</button>
	    <button type="button" class="btn btn-success" @click='save'>Save</button>
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
    sortKey: String,
    columns:Array,
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
      columns:[
          {name: 'email', title: 'Email', type: 'text'},
          {name: 'sex', title: 'Sex', type: 'select', options: ['M', 'F']},
          {name: 'email', title: 'Email', type: 'text'}]
    }
  },
  computed: {
    isSelectedAll: {
      get: function () {
        var isCheckAll = true
        for (var i in this.gridData) {
          var item = this.gridData[i]
          if (!item.isChecked) {
            isCheckAll = false
            break
          }
        }
        return isCheckAll
      },
      set: function (newValue) {
        console.log('set newValue:', newValue)
        for (var i in this.gridData) {
          var item = this.gridData[i]
          Vue.set(item, 'isChecked', newValue)
        }
      }
    }
  },
  methods: {
    sortBy: function (key) {
      console.log('click sortBy:', key)
      this.sortKey = key
      var self = this
      var newSort = this.sortOrders[key] ? (this.sortOrders[key] * -1) : -1
      var orders = {}
      this.columns.forEach(function (k) {
        var keyName = k.name
        console.log(k.name === key)
        if (keyName === key) {
          self.order = (newSort < 0 ? 'ASC' : 'DESC')
          orders[keyName] = newSort
        } else {
          orders[keyName] = 1
        }
      })
      this.$set('sortOrders', orders)
    },
    select: function (entry) {
      this.selectedRow = entry
    },
    edit: function () {
      console.log('edit')
      this.showEditModal = true
    },
    deletes: function () {
      console.log('delete')
    },
    add: function () {
      console.log('edit')
    },
    save: function () {
      console.log('save')
      this.showEditModal = false
      var editGridData = []
      for (var i in this.gridData) {
        var tmp = this.gridData[i]
        if (tmp.isChecked) {
          editGridData.push(tmp)
        }
      }
      this.onSave(editGridData)
    }
  }
}

</script>
