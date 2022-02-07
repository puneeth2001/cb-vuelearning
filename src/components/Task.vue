<template>
    <div :class="[task.reminder ? 'reminder' : '','task']">
        <h3>{{task.text}}
          <span class="fa-stack fa-1x">
            <i @click="onDelete(task.id)" class="fas fa-times "></i> 
            <i @click="onEdit(task.id)" class="fas fa-pen-alt"></i></span> 
            </h3>

        <p>{{ task.memberRole}}</p>
    </div>
</template>

<script>
export default {
    name: 'Task',
    props: {
        task: Object
    },
    methods: {
      onDelete(id){
        this.$emit('delete-task', id)
      },
      onEdit(id){
        this.$emit('edit-task',id)
      }
    }
}
</script>

<style scope>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>