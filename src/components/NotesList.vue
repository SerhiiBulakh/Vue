<template>
<div> 
    <div class="btn-group" style="margin: 1%;">
        <button class="btn btn-primary btn-lg active" @click="sortData('title')">Sort by title</button>
       <button class="btn btn-primary btn-lg active" @click="sortData('date')">Sort by date</button>
    </div>


    <div class="col-sm-12">
        <div class="col-sm-4 note" v-for="(note, index) in notes">
            <div class="card">
                <div class="card-block">
                    <div class="btn-group " style="float: right;">
                            <button class="btn btn-primary" @click="removeNote(index)">x</button>
                            <button class="btn btn-primary" @click="duplicateNote(index)">Duplicate</button>
                    </div>
                            
                    
                    
                    <h4 class="card-title">{{ note.title }}</h4>
                    <h6 class="card-subtitle mb-2 text-muted">{{ note.email }}</h6>
                    <h6 class="card-subtitle mb-2 text-muted">{{note.date | formatDate}}</h6>
                    <p class="card-text">{{note.text}}</p>
                </div>
            </div>
        </div>
    </div>

</div>
</template>

<script>
export default {
  name: 'NotesList',
  props:['notes'],
  methods: {
       duplicateNote(index) {
               let { text, title, email, date } = this.notes[index]
               title +='Copy'
               date = new Date()
               this.notes.push({text, title, email, date})
               
            },
            removeNote(index){
                this.notes.splice(index, 1)
            },
         
            
            sortData(type) {
                if(type === 'date') return this.notes.sort( (a, b) => new Date(b.date) - new Date(a.date));
                return this.notes.sort( (a, b) => {
                    if (a[type] > b[type]) {
                            return 1;
                    }
                    if (a[type] < b[type]) {
                            return -1;
                    }
 
                    return 0;
                })
            }
  },
  filters:{
        
    formatDate(date) {
                const day=date.getDate();
                const month=date.getMonth() + 1;
                const year=date.getFullYear();
                const today = `${day}.${month < 10 ? `0${month}` : month}.${year}`
                return today
            }
  }
  
};
</script>


<style scoped>

</style>