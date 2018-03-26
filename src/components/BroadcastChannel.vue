<template>
  <div class="bc">
    <p>{{lastUpdatedTime}}</p>
    <button @click="updatedTime">Click Me !</button>
  </div>
</template>

<script>
export default {
  name: 'bc',
  data () {
    return {
      lastUpdatedTime: null,
      bc: null,
    }
  },
  created(){
    this.bc = new BroadcastChannel('test_bc_channel')
    this.bc.onmessage = (event) => {
      console.log('message receive: ', event.data)
      this.lastUpdatedTime = event.data
    }
  },
  destroyed(){
    this.bc.close()
  },
  methods:{
    updatedTime(){
      this.bc.postMessage(+ new Date())
    }
  }
}
</script>
