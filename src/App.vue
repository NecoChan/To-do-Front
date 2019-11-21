<template>
    <div class="root">
        {{test}}

        <ul>
          <li v-for="(task, index) in taskList">
         	  {{ task }}
          <button type="button" class="close" @click="remove(index)">
            <span aria-hidden="true">&times;</span>
          </button>
          </li>
        </ul>
        <input type="text" placeholder="Что добавить?" v-model="formText">
        <button type="button" @click="add">добавить</button>
       
    </div>
</template>

<script>


    export default {
        data: function () {
            return {
                test: 'Список задач:',
                taskList: ['Django','MySQL','Математика'],
                formText: ''
            }
        },
        methods: {
          add: function () {
            this.taskList.push(this.formText);
            // вызываем созданный нами метод внутри метода “add”
            this.save();
            // сбрасываем значение формы сразу после добавления
            this.formText = null;
            // валидируем пользовательский ввод
            if(!this.formText) {
              return;
            }

            },
            // метод, реализующий сохранение массива в локальное хранилище
            save: function () {
              localStorage.setItem('tasks', JSON.stringify(this.taskList));
            },





        },
        created() {
          let storageData = localStorage.getItem('tasks');
          console.log(storageData);
          // this.taskList = JSON.parse(storageData);
          localStorage.getItem('tasks')
          this.taskList.push()
          if(storageData) {
          }
        },
        remove: function (index) {
            this.taskList.splice(index, 1);
            this.save();
        }


        }

</script>

<style>
  body {padding:20px;}
</style>
