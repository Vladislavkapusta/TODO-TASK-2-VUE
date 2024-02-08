<template>
    <div>
        <div class="add-layout">
            <div class="inputs">
                <select v-model="selectedDay">
                    <option value="ПН">Понедельник</option>
                    <option value="ВТ">Вторник</option>
                    <option value="СР">Среда</option>
                    <option value="ЧТ">Четверг</option>
                    <option value="ПТ">Пятница</option>
                    <option value="СБ">Суббота</option>
                    <option value="ВС">Воскресенье</option>
                </select>
                <select v-model="selectedPriority">
                    <option value="important">Важная</option>
                    <option value="not-important">Неважная</option>
                </select>
                <input type="text" v-model="taskName" placeholder="Название задачи">
            </div>
            <div class="button-space">
            <button class="add-button" @click="addTask">Добавить</button>
            </div>
        </div>
      
  
      <h2>Список задач</h2>
      <div class="day-layout" v-for="(day, index) in days" :key="index">
        <div class="day">
            <h3>{{ day }}</h3>
        </div>
        <div class="tasks">
            <div v-for="task in tasks.filter(task => task.day === day)" :key="task.id" @mouseover="highlight(task)" @mouseleave="unhighlight(task)">
                <span :style="{ color: task.priority === 'important' ? 'red' : 'green' }">{{ task.name }}</span>
                <button @click="removeTask(task)">Удалить задачу</button>
            </div>
            
            <button @click="removeAllTasks(day)">Удалить все задачи</button>
        </div>

      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        taskName: '',
        selectedDay: 'Понедельник',
        selectedPriority: 'important',
        tasks: [
          { id: 1, name: 'Срочное дело', priority: 'important', day: 'ПН' },
          { id: 2, name: 'Подготовить отчет', priority: 'not-important', day: 'ВТ' },
          // Добавьте ваши задачи здесь
        ],
        days: ['ПН', 'ВТ', 'СР', 'ЧТ', 'ПТ', 'СБ', 'ВС']
      };
    },
    methods: {
      addTask() {
        if (this.taskName.trim() === '') {
          return;
        }
        this.tasks.push({
          id: this.tasks.length + 1,
          name: this.taskName,
          priority: this.selectedPriority,
          day: this.selectedDay
        });
        this.taskName = '';
      },
      removeTask(task) {
        this.tasks = this.tasks.filter(t => t !== task);
      },
      removeAllTasks(day) {
        this.tasks = this.tasks.filter(task => task.day !== day);
      },
      highlight(task) {
        task.showDeleteButton = true;
      },
      unhighlight(task) {
        task.showDeleteButton = false;
      }
    }
  };
  </script>
  
  <style scoped>

  .day-layout{
    display: flex;
    flex-direction: row;

    width: 1088px;
    min-height: 70px;
    border-radius: 20px;

    background: #ECF0F1;
  }

  input{
    width: 520px;
    height: 45px;

    font-size: 20px;
    margin-left: 20px;
  }

  select{
    width: 250px;
    height: 45px;

    margin-left: 20px;
    font-size: 20px;
  }
  .add-layout{
    width:1088px;
    height: 178px;

    display: flex;
    flex-direction: row;

    border-radius: 10px;

    background: #ECF0F1;


  }

  .button-space{
    align-self: flex-end;
    width: 40%;
    position: relative;

  }

  .inputs{
    display: flex;
    flex-direction: row;

    flex-wrap: wrap;
    width: 60%;

    align-items: center;
    justify-content: center;
    
  }

.add-button{
    width: 163px;
    height: 45px;
    border-radius: 23px;
    border: 1px solid black;

    background: #1ABC9C;

    color: #ECF0F1;

    position: absolute;

    right: 35px;
    bottom: 20px;

    font-size: 20px;

}
  
  button:focus {
    outline: none;
  }
  </style>