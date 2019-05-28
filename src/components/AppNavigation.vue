<template>
<span>
    <v-navigation-drawer app v-model="drawer" class="brown lighten-2" dark disable-resize-watcher>
            <v-list>
                <template v-for="(item, index) in items">
                    <v-list-tile  :key="index"
                                  router
                                   :to="item.link">
                        <v-list-tile-content>
                            {{item.title}}
                        </v-list-tile-content>
                    </v-list-tile>
                    <v-divider :key="`divider-${index}`"></v-divider>
                </template>
            </v-list>
        </v-navigation-drawer>
    <v-toolbar app color='brown darken-4' dark>
        <v-toolbar-side-icon class="hidden-md-and-up" 
            @click="drawer = !drawer"></v-toolbar-side-icon>
        <v-spacer class="hidden-md-and-up"></v-spacer>
        <router-link to='/'>
        <v-toolbar-title>{{appTitle}}</v-toolbar-title>   
        </router-link>
        <v-btn flat class="hidden-sm-and-down" to='/menu'>Menu</v-btn>
        <v-spacer class="hidden-sm-and-down"></v-spacer>
        <div class="hidden-sm-and-down" v-if="!isAuthenticated">
        <v-btn flat to='/sign-in'>SIGN IN</v-btn>
        <v-btn color="brown lighten-3" to='/join'>JOIN</v-btn>
        </div>
        <div v-else>
        <v-btn outline color="white"  @click="logout">LOGOUT</v-btn>
        <v-btn flat to='/about'>Profile</v-btn>
        </div>
    </v-toolbar>
</span>
</template>

<script>
export default {
    name: 'AppNavigation',
    data() {
        return {
            appTitle: 'Meal Prep',
            drawer: false,
            items: [
                {title: 'Menu', link: '/menu'},
                {title: 'Profile', link: '/about'},
                {title: 'Sign In', link: '/signin'},
                {title: 'Join', link: 'join'}
            ]
        };
    },
    computed: {
        isAuthenticated(){
            return this.$store.getters.isAuthenticated;
        }
    },
    methods: {
        logout() {
            this.$store.dispatch('userSignOut');
        }
    }
}
</script>

<style scoped>
a{
    color:white;
    text-decoration: none;
}
</style>
