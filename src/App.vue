<script setup>
import { ref } from 'vue';

const form = ref(false);
const newNote = ref("");
const notesArr = ref([]);
const selectedId = ref(""); 
const viewNote = ref({});
const viewStatus = ref(false)

const addNote = () => {
  form.value = false;
  viewStatus.value = false;
  if (newNote.value.length > 0) {
    notesArr.value.push({
      id: Math.random() * 1000000,
      text: newNote.value,
      date: new Date(),
    });
  }
  newNote.value = "";
};

const openNote = (itemId) => {
  selectedId.value = itemId;
  viewStatus.value = true
  viewNote.value = notesArr.value.find((item) => item.id == itemId)
  console.log(viewNote.value)
};
</script>


<template>
  <main>

      <div v-if="form" class="input-container">
       <div class="exit" @click="form = false"><i class='bx bx-x'></i></div>
       <textarea name="noteInput" v-model="newNote"></textarea>
       <button type="submit" @click="addNote()">Add Note</button>
      </div>


      <div v-if="viewStatus" class="input-container">
         <div class="exit" @click="viewStatus = false"><i class='bx bx-x'></i></div>
         <textarea name="noteInput" v-model="viewNote.text"></textarea>
         <button type="submit" @click="addNote()">Add Note</button>
      </div>

      
    <section>
      <header>
        <h1>Notes</h1>
        <i @click="form = true" class='bx bx-message-alt-add'></i>
      </header>
      <div class="display">
        <div class="card" v-for="(item, index) in notesArr" :key="index" @click="openNote(item.id)">
          <h3>{{item.text}}</h3>
          <p>{{ item.date.toLocaleDateString("en-US") }} </p>

        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Kablammo&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Patrick+Hand&display=swap');
main{
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: center;
}
section{
  height: 100%;
  width: 80%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
header{
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  margin-top: 3em;
  color: white;
}
header>h1{
  font-size: 6em;
  font-family: 'Kablammo',sans-serif;
}
header>i{
  font-size: 4em;
}
.display{
  width: 100%;
  margin-top: 4em;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  color: white;
  gap: 2em;
}
.card{
  width: 25rem;
  height: 17rem;
  box-shadow: 0px 1px 8px 1px rgba(0, 0, 0, 0.5);
  display: grid;
  grid-template-rows: 80% 5%;
  justify-content: space-between;
  font-size: 1.5em;
  font-family: 'Patrick Hand',sans-serif;
}
.card>h3{
  overflow: hidden;
}
form{
  position: absolute;
  width: 40%;
  top: 10em;
  display: flex;
  flex-direction: column;
 
}
form>p{
  font-size: 2.5em;
  text-align: end;
}
textarea{
  resize: none;
  outline: none;
  background: #F79327;
  font-size: 2em;
  width: 95%;
  height: 60%;
  border: 1px solid #525FE1;
   font-family: 'Patrick Hand',sans-serif;
   color: white;
}

.input-container{
  position: absolute;
  width: 70%;
  height: 60%;
  top: 10em;
  background: #525FE1;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  border-radius: 1em;
}
.exit{
  font-size: 3em;
  color: white;
}
.input-container>button{
  width: 60%;
  font-size: 1.5em;
  padding: 0.5em;
  background: #F79327;
  border: 0px;
  color: white;
}
</style>