<template>
     <div class="form">
        <p v-if="errors.length" >
            <b>Пожалуйста исправьте указанные ошибки:</b>
            <ul>
                <li v-for="error in errors">{{ error }}</li>
            </ul>
        </p>
        <div class="form-group">
            <label>Note title</label>
            <input
                     
                    class="form-control"
                    type="text"
                    v-model="note.title"
            >
        </div>
        <div class="form-group">
            <label>Email</label>
            <input
                     
                    class="form-control"
                    type="email"
                    v-model="note.email"
            >
        </div>
        <div class="form-group">
            <label>Note text</label>
            <input 
                    
                    class="form-control"
                    type="text"
                    v-model="note.text"
            >
        </div>
         
        <button :disabled="disabledButton()"
                class="btn btn-primary"
                @click="addNote">Submit</button>
    </div>
</template>

<script>
export default {
  name: 'NotesForm',
  props: {
    msg: String,
  },
  data() {
     return {
         note: {
                title: '',
                text: '',
                email: ''
            },
            errors:[]
     }  
  },
  methods: {
        addNote(){
                let { text, title, email } = this.note;
                
                if(this.validateFields(title, email, text)) {
                     this.$emit('addNote', {
                            text,
                            email,
                            title,
                            date: new Date()
                    })
                    this.cleanFields()
                }
               
            },
           
        validateFields(title, email, text) {
                
                this.errors = [];
                if (!this.isFirstLetterUppercase(title) || title.length < 3){
                        this.errors.push('Заголовок должен начинатся с заглавной буквы и не меньше трех символов');
                }

                if(text.length < 6) {
                    this.errors.push('Тест должен быть не меньше шести символов');
                }
                if(!this.validEmail(email)) {
                    this.errors.push('Email не валидный');
                }

                if (!this.errors.length) {
                    return true;
                }
            },
            validEmail (email) {
                const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
                return re.test(email);
            },
            isFirstLetterUppercase(word) {
                return /^[A-Z]/.test(word)
            },
            disabledButton(bool = true) {
                if(this.note.text.length && this.note.title.length && this.note.email.length) return false
                return true
            },  
               cleanFields() {
                this.note.title = ''
                this.note.text = ''
                this.note.email = ''
            }
  },
};
</script>


<style scoped>

</style>