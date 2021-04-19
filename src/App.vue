<template>
  <div class="app">
    <Form @submitForm="addNewItem" />
    <total-balance :total="totalBalance"></total-balance>
    <sort-list @income-sort="incomePer" @outcome-sort="outcomePer" @all-sort="allPer"></sort-list>
    <budget-list :list="list">
      <budget-list-item
      @mark="openPop"
      v-for="item in sortedItems"
      :key="item.id"
      :item_data="item"
      ></budget-list-item>
    </budget-list>
    <confirm-del :visible="visible" @confirm-del="confirmDelete" @cancel-del="cancelDel"></confirm-del>
</div>
</template>



<script>
import BudgetList from '@/components/BudgetList'
import TotalBalance from '@/components/TotalBalance'
import Form from '@/components/Form'
import BudgetListItem from '@/components/BudgetListItem'
import ConfirmDel from '@/components/ConfirmDel'
import SortList from '@/components/SortList'
const sortFunctions = {
  all(arr) {
    return arr
  },
  income(arr) {
    return Object.entries(arr).filter(([,value]) => value.type === "INCOME").reduce((acc, [key,value]) => {
        acc[key] = value
        return acc
      }, {})
  },
  outcome(arr) {
    return Object.entries(arr).filter(([,value]) => value.type === "OUTCOME").reduce((acc, [key,value]) => {
        acc[key] = value
        return acc
      }, {})
  }
}
export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    Form,
    BudgetListItem,
    ConfirmDel,
    SortList
  },
  data() {
    return {
      visible: false,
      idItem: null,
      permission: 'all',
      list: {
        1: {
          type: "INCOME",
          value: 100,
          comment: "Some income comment",
          id: 1
        },
        2: {
          type: "OUTCOME",
          value: -75,
          comment: "Some outcome comment",
          id: 2
        }
      },

    }
  },
  methods: {
    openPop (id) {
      this.visible = true
      this.idItem = id
      console.log(this.sortedItems)
    },
    deleteItem(id) {
        for (let i in this.list) {
          if (this.list[i].id === id) {
            delete this.list[i]
            break
          }
        }
    },
    cancelDel () {
      this.visible = false
    },
    confirmDelete () {
      this.visible = false
      this.deleteItem(this.idItem)
    },
     mounted() {

    },
    addNewItem(data) {
      const newObj = {
          ...data,
          id: (Math.random() * 10000).toFixed(0)
      }
      this.list[newObj.id] = newObj
    },
    incomePer() {
      this.permission = 'income'
    },
    outcomePer() {
      this.permission = 'outcome'
    },
    allPer() {
      this.permission = 'all'
    },

  },
  computed: {
    totalBalance () {
      return Object.values(this.list).reduce((acc, item) => {
        return acc + item.value
      }, 0)
    },
    sortedItems() {
      return sortFunctions[this.permission](this.list);
    }
  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 500px;
  margin: 60px auto 0;
}
</style>
