<template lang="html">
  <div class="">
    <!-- Modal -->
   <div class="modal fade" id="myModal2" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
     <div class="modal-dialog" role="document">
       <div class="modal-content">
         <div class="modal-header">
           <h3 class="modal-title" id="exampleModalLabel">Details task "{{ dataTask.title }}" for {{ dataTask.assign_to }}</h3>
           <button type="button" class="close" data-dismiss="modal">
             <span aria-hidden="true">&times;</span>
           </button>
         </div>
         <div class="modal-body">
          Task Description: {{ dataTask.description }},
          Task Point: {{ dataTask.point }},
          Status: {{ dataTask.status}}
         </div>
         <div class="modal-footer">
           <button type="button" class="btn btn-danger" data-dismiss="modal" @click="remove(dataTask['.key'])">delete</button>
           <button type="button" class="btn btn-primary" data-dismiss="modal" @click="moveToTodo(dataTask['.key'], dataTask.title, dataTask.description, dataTask.point, dataTask.assign_to)">todo</button>
         </div>
       </div>
     </div>
   </div>
  </div>
  </div>
</template>

<script>
export default {
  props: ['dataTask'],
  methods: {
    remove (id) {
      if (window.confirm('delete this task')) {
        this.$db.ref('task/log/' + id).remove()
      }
    },
    moveToTodo (id, title, description, point, assign) {
      if (window.confirm('move to todo')) {
        this.$db.ref('task/todo').push({
          title: title,
          description: description,
          point: point,
          assign_to: assign,
          status: 'todo'
        })
        this.$db.ref('task/log/' + id).remove()
      }
    }
  }
}
</script>

<style lang="css">
</style>
