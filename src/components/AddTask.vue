<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Email</label>
      <input type="text" v-model="text" name="text" placeholder="Add Member" />
    </div>
      <div class="form-check">
        <input class="form-check-input" type="radio" id="TechSupportRadio"
                v-model="memberRole" name="memberRole" value="Tech Support">
        <label class="form-check-label" for="TechSupportRadio">
          <span class="fw-bold">Tech Support</span> 
        </label>
        <hr>
      </div>

      <div class="form-check">
        <input class="form-check-input" type="radio" id="AnalystRadio" v-model="memberRole"
                name="memberRole" value="Analyst">
        <label class="form-check-label" for="AnalystRadio">
          <span class="fw-bold">Analyst</span>
        </label>
        <hr>
      </div>

      <div class="form-check">
        <input class="form-check-input" type="radio" id="AdminRadio" v-model="memberRole"
                name="memberRole" value="Admin">
        <label class="form-check-label" for="AdminRadio">
          <span class="fw-bold">Admin</span>
        </label>
      </div>

    <input type="submit" value="Save Member" class="btn btn-block" />
  </form>
</template>

<script>
export default {
    name: 'AddTask',
    data(){
        return {
            text: '',
            day: '',
            memberRole: '',
        }
    },
    methods:{
        onSubmit(e){
            e.preventDefault()

            if(!this.text){
                alert('please add a task!')
                return
            }
            const newTask = {
                id: Math.floor(Math.random()*10000),
                text: this.text,
                day: this.day,
                memberRole: this.memberRole, 
            }

            this.$emit('add-task',newTask);

        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>