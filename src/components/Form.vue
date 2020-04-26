<template>
  <div class="form-body">
    <h1>Add Task Card</h1>
    <!-- <span><p>aa</p></span> -->
    <div class="err">
        <div v-bind:class="{ text: isErrTitle }">
            <p v-if="isErrTitle">Min 3 and max 40 character for Title!</p>
        </div>
        <div v-bind:class="{ text: isErrDesc }">
            <p v-if="isErrDesc">Min 33 and max 255 character for Description!</p>
        </div>
    </div>
    <form @submit="addCard">
        <input @input="onTitleInput" type="text" v-model="title" name="title" class="title" placeholder="Title...">
        <input @input="onDescInput" type="text" v-model="description" name="description" class="desc" placeholder="Description...">
        <div class="bottom">
            <input type="datetime-local" v-model="date" name="date">
            <input type="submit" value="Submit">
        </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Form',
  data(){
      return {
          title: '',
          description: '',
          date: '',
          isErrTitle: false,
          isErrDesc: false
      }
  },
  methods: {
      addCard(e){
        e.preventDefault()
        if (!this.isErrTitle && !this.isErrDesc && this.date != ''){
            const newCard = {
                title: this.title,
                description: this.description,
                date: this.date
            }
            console.log(newCard)
            this.$emit('add-card', newCard)
            this.title = '';
            this.description = '';
            this.date = ''
        }else{
            alert('Sorry, please make sure the form filled correctly');
        }
      },

      onTitleInput(){
          console.log(this.title.length)
          if (this.title.length < 3 || this.title.length > 30){
              this.isErrTitle = true
          }else{
              this.isErrTitle = false
          }
      },

      onDescInput(){
          console.log(this.description.length)
          if (this.description.length < 3 || this.description.length > 255){
              this.isErrDesc = true
          }else{
              this.isErrDesc = false
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
    color:rgb(63, 63, 63);
    box-shadow:  4px 2px 5px 0px #ccc;
}

.form-body{
    background: rgb(235, 235, 235);
    width: 50vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-bottom: 20px;
    box-shadow: 0px 0px 5px 1px grey;
    border-radius: 15px;
}

.form-body form{
    margin: 0 0;
    padding: 0;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    height: 200px;
}

.form-body .err{
    width: 90%;
    height: 50px;
}

.form-body .err .text{
    color: red;
    font-size: 12px;
}

.form-body form input[type=text]{
    min-width: 90%;
    max-width: 90%;
    outline: none;
    border-radius: 4px;
    border: none;
    padding: 7px;
}

.form-body form input[type=datetime-local]{
    outline: none;
    border-radius: 4px;
    border: none;
    padding: 7px;
}

.form-body form input[type=submit]{
    color: rgb(255, 255, 255);
    font-weight: bold;
    width: 80px;
    border-radius: 4px;
    border: none;
    background: rgb(151, 151, 151);
    outline: none;
}

.form-body form input[type=submit]:hover{
    cursor: pointer;
    background: rgb(235, 235, 235);
    color: rgb(59, 59, 59);
    box-shadow: 0px 0px 10px 4px grey;
    transition: 0.5s;
}

.form-body form .desc{
    min-height: 40px;
}

.form-body form .bottom{
    width: 50%;
    display: flex;
    justify-content: space-evenly;
}

</style>
