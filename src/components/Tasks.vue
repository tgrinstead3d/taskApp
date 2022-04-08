<template>
  <div class="wrapper">
    <div class="drop-zone" @drop="onDrop($event, 1)" @dragover.prevent @dragenter.prevent>
      <h3>Not Started</h3>
      <div class="drag-el" v-for="item in listOne" :key="item.title" draggable="true" @dragstart="startDrag($event, item)">
        {{ item.title }}
      </div>
    </div>
    <div class="drop-zone" @drop="onDrop($event, 2)" @dragover.prevent @dragenter.prevent>
      <h3>In Progress</h3>
      <div class="drag-el" v-for="item in listTwo" :key="item.title" draggable="true" @dragstart="startDrag($event, item)">
        {{ item.title }}
      </div>
    </div>
    <div class="drop-zone" @drop="onDrop($event, 3)" @dragover.prevent @dragenter.prevent>
      <h3>Completed</h3>
      <div class="drag-el" v-for="item in listThree" :key="item.title" draggable="true" @dragstart="startDrag($event, item)">
        {{ item.title }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      items: [
        {
          id: 0,
          title: 'First Task',
          list: 1
        },
        {
          id: 1,
          title: 'Second Task',
          list: 1
        },
        {
          id: 2,
          title: 'Third Task',
          list: 2
        }]
    }
  },
  computed: {
    listOne () {
      return this.items.filter(item => item.list === 1)
    },
    listTwo () {
      return this.items.filter(item => item.list === 2)
    },
    listThree () {
      return this.items.filter(item => item.list === 3)
    }
  },
  methods: {
    startDrag (evt, item) {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemID', item.id)
    },
    onDrop (evt, list) {
      const itemID = evt.dataTransfer.getData('itemID')
      const item = this.items.find(item => item.id == itemID)
      item.list = list
    }
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  max-width: 350px;
  background-color: rgba(198,198,198,0.7);
  padding-top: 10px;
  padding-bottom: 10px;
}
.drop-zone {
  background-color: #f3f3f3;
  margin-bottom: 10px;
  padding: 10px;
  min-width: 300px;
  border-radius: 8px;
  box-shadow: rgba(0,0,0,0.25) 2px 0 6px;
  font-weight: 400;
}

.drag-el {
  background-color: #fff;
  margin-bottom: 10px;
  padding: 5px;
  color: #282828;
  border-radius: 6px;
  /*border: #888888 solid 1px;*/
  font-weight: 300;
  box-shadow: rgba(0,0,0,0.35) 0 0 5px;
}
</style>
