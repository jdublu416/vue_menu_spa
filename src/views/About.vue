<template>
    <v-container fluid>
        <v-layout column>
            <h1 class="title my-3">My Recipes</h1>
            <div v-for="(item, idx) in userRecipes" class="subheading mb-2"
            :key="idx">{{item}}</div>
            <v-btn to="/menu" color="primary" class="mybtn">Go to Menu</v-btn>
        </v-layout>
    </v-container>
</template>

<script>
export default {
    name: 'About',
   computed: {
       userRecipes(){
           return this.$store.state.userRecipes;
       }
   },
   mounted() {
       this.getRecipes();
   },
   methods: {
       getRecipes(){
           this.$store.dispatch('getUserRecipes');
       }
   }
}
</script>

<style scoped>
.mybtn{
    width: 100px;
}
</style>


