<template>
  <div id="app">
    <Form v-on:add-card="addNewCard"></Form>
    <div v-if="cards.length != 0">
      <select @change="onSort($event)" name="sort">
        <option value=0>Latest</option>
        <option value=1>Oldest</option>
      </select>
    </div>
    <div class="cards" v-bind:class="{ reverse: isReverse, noreverse: isNoReverse}">
      <div class="card" v-for="card in cards" :key="card.title">
        <div class="head">
          <h3>{{card.title}}</h3>
          <h5>{{card.date}}</h5>
        </div>
        <div class="body">
          <p>{{card.description}}</p>
        </div>
    </div>
    </div>
  </div>
</template>

<script>
import Form from './components/Form';

export default {
  name: 'App',
  components: {
    Form
  },
  data(){
    return({
      cards: [
      ],
      isReverse: false,
      isNoReverse: true
    })
  },
  methods:{
    addNewCard(new_card){
      // const { title, description, date } = new_card;
      //this.cards = [...this.cards,new_card];
      let new_date = new Date(new_card.date);
      if(this.cards.length != 0){
        console.log('this.cards')
        for (let i = 0; i < this.cards.length; i++){
          let current_date = new Date(this.cards[i].date)
          if (new_date < current_date){
            if(i === 0){
              console.log('this.cards unshift')
              this.cards.unshift(new_card)
              break
            }
            else{
              console.log('this.cards splice lower')
              this.cards.splice(i-1,0,new_card)
              break
            }
          }
          else{
            if(i === 0 || i === this.cards.length){
              console.log('this.cards push')
              this.cards.push(new_card)
              break
            }
            else{
              console.log('this.cards splice more')
              this.cards.splice(i+1,0,new_card)
              break
            }
          }
        }
      }
      else{
        console.log('not this.cards')
        this.cards = [...this.cards,new_card];
      }
      console.log(this.cards)
    },

    onSort(e){
      console.log(e.target.value)
      this.isReverse = !this.isReverse
      this.isNoReverse = !this.isNoReverse
    }
  }
}
</script>

<style>
body{
  margin: 0;
}

#app {
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-image: linear-gradient(rgb(143, 143, 143), rgb(255, 255, 255));
  min-height: 100vh;
  background-repeat: no-repeat;
  background-attachment: fixed;
  overflow-x: hidden;
}

.cards{
  margin-top: 20px;
  width: 100vw;
  display: flex;
  justify-content: space-around;
  align-content: flex-start;
  flex-wrap: wrap;
  margin-bottom: 40px;
}

.reverse{
  flex-direction: row-reverse;
}

.noreverse{
  flex-direction: row;
}

.card{
  width: 400px;
  border-radius: 10px;
  background: rgb(233, 233, 233);
  padding: 0;
  margin: 20px 0 0 0;
  display: flex;
  flex-direction: column;
  box-shadow: 0px 0px 50px 4px rgb(150, 150, 150);
}

.card h3{
  color: rgb(77, 77, 77);
}

.card h5{
  color: rgb(124, 124, 124);
  font-weight: 100;
}

.card p{
  color: rgb(77, 77, 77);
}

.card .head{
  display: flex;
  justify-content: space-between;
  padding: 0px 10px;
  border-bottom: 1px solid rgb(163, 163, 163);
}

.card .body{
  padding: 0px 10px;
  min-height: 100px;
}
</style>
