<script>
export default {
  data() {
    return {
      tasks: [],
      newTask: '',
    };
  },
  methods: {
    addTask() {
      if (this.newTask === '') {
        alert('This field cannot be empty');        
      } else {
        this.tasks.push({ title: this.newTask, checked:false });
        this.newTask = '';
        this.saveData();
      }
    },
    toggleChecked(task){
      task.checked = !task.checked;
      console.log(task.checked);
      this.saveData();
    },
    deleteTask(index){
      this.tasks.splice(index,1)
      console.log(index)
      this.saveData();
    },

    saveData(){
      localStorage.setItem('data',JSON.stringify(this.tasks));
      
    }
    ,
    loadData(){
      const savedData = localStorage.getItem('data')
      if (savedData){
        this.tasks = JSON.parse(savedData);
      }
    }
  }
    ,
    mounted(){     
      this.loadData();
    } 
    

  
};
</script>

<template>
  <div class="container">
    <div class="to-do">
      <h2>To-Do List</h2>
      <div class="row">
        <input 
          type="text" 
          id="input-box" 
          placeholder="Add your task" 
          v-model="newTask"  
        />
        <button @click="addTask">Add Task</button>
      </div>

      <ul id="list-container" ref="list-container">
        <li 
          v-for="(task, index) in tasks" 
          :key="index" 
          v-bind:class="{checked: task.checked }"
          @click="toggleChecked(task)">  {{ task.title }}  
            
             <i class="fa-solid fa-x"  @click="deleteTask(index)"></i> 
             
        </li> <!-- Iterate over tasks -->
      </ul>
    </div>
  </div>
</template>

<style scoped>
*{
    margin: 0;
    padding: 0;
    font-family: 'poppins';
    box-sizing: border-box;
}

.container{
    width: 100%;
    height: 100vh;
    background: linear-gradient(140deg, #153677, #4e085f);
    padding: 10px;
}

.to-do{
    width: 100%;
    max-width: 540px;
    background: #ffff;
    margin: 100px auto 20px;
    padding: 30px ;
    border-radius: 30px;
}

.to-do h2{
    color: #002765;
    display: flex;
    align-items: center;
    margin-bottom: 20px;
}

.to-do h2 img{
    width: 30px;
    margin-left: 10px;
}

.row{
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #edeef0;
    border-radius: 30px;
    padding-left: 20px;
    margin-bottom: 25px;
}

input{
    flex:1;
    border:0;
    outline: none;
    background: transparent;
    padding: 10px;
    
}

button{
    border: none;
    outline: none;
    padding: 16px 50px;
    background: #ff5945;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
    border-radius: 40px;
}

ul li{
    list-style: none;
    font-size: 17px;
    padding: 12px 8px 12px 50px;
    cursor: pointer;
    user-select:none;
    position: relative;
}

ul li::before{
    content: '';
    position:absolute;
    height: 28px;
    width: 28px;
    border-radius: 50%;
    background-image: url(/src/assets/images/unchecked.png);
    background-size: cover;
    background-position: center;
    top: 12px;
    left: 8px;

}


ul li.checked{
    color: #555;
    text-decoration: line-through;

}

ul li.checked::before{
    background-image: url(/src/assets/images/checked.png);
}

ul li i{
    right: 0;
    font-size: 16px;
    position: absolute;  
    font-weight: 0;

}

ul li i:hover{
    
    transition: ease-in 0.2s;
    color: #1f90b3;
}

</style>
