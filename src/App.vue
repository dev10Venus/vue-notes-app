
<script setup>
import { ref } from 'vue'
const showModal = ref(false)
const newNote = ref('')
const notes = ref([])
const errorMessage = ref('')
const getRandomColor = () =>{
  let color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}
const addNote = () => {
  if(newNote.value.length<10){
    errorMessage.value = 'Note must be at least 10 characters long';
    return;
  }
  notes.value.push({
    id: notes.value.length + 1,
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()
  });
  newNote.value = '';
  showModal.value = false;
  errorMessage.value = '';
}
const clickShowModal = () => {
  showModal.value = true;

}

</script>
<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea name="note" v-model.trim="newNote" id="note"  cols="30" rows="10"></textarea>
        <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button @click="showModal=false" class="close">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        
        <h1>
          Notes
        </h1>
        <button @click="clickShowModal">+</button>
      </header>
      <div class="cards-container">
        <div class="card" v-for="note in notes" :key="note.id" :style="{backgroundColor:note.backgroundColor}" >
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">
            {{ note.date.toLocaleDateString('en-BD') }}
          </p>
        </div>
         
      </div>
    </div>
  </main>
</template>

<style scoped>
main{
  width: 100vw;
  height: 100vh;
}
.container{
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}
header button{
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21,20,20);
  color: white;
  border-radius: 100%;
  font-size: 20px;
}
.cards-container{
  display: flex;
  flex-wrap: wrap;
}
.error{
  color: red;
  font-size: 12px;
  margin-top: 5px;
}
.card{
  width: 225px;
  height: 225px;
  /* background-color: rgb(231, 94, 30); */
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.date{
  font-size: 12px;
  color: rgb(21,20,20);
  font-weight: bold;
}
.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.77);
  z-index: 10;
  display:flex;
  align-items: center;
  justify-content: center;
}
.modal{
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button{
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px; 
}
.modal .close{
  background-color: rgb(193, 15, 15);
  margin-top: 7px;
}
</style>