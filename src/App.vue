<template>
  <div id="app">
    <NotesForm @addNote='addNote' />
    <NotesList :notes='notes' />
  </div>
</template>

<script>
import NotesForm from './components/NotesForm.vue';
import NotesList from './components/NotesList.vue';

export default {
  name: 'app',
  components: {
    NotesForm,
    NotesList
  },
  data() {
    return {
       notes: [
                {
                    title: 'Visited Hawaii',
                    text: 'I loved the beaches and delicious fresh coconuts',
                    date: new Date()
                },
                {
                    title: 'Visited London',
                    text: 'I loved the beaches and delicious fresh coconuts',
                    date: new Date()
                },
                {
                    title: 'Visited Dnipro',
                    text: 'I loved the beaches and delicious fresh coconuts',
                    date: new Date()
                }
            ]
    }
  },
  methods: {
    addNote ({text, email, title, date}) {
        this.notes.push({text, email, title, date}) 
    }
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
