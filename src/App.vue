<!-- Html XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX-->
<template>

    <v-app id="inspire">

        <!-- Menu lateral xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
        <v-navigation-drawer v-model="drawer" app>

            <!-- Título + Subtítulo ------------------------------------------------------------------------------------------------------------------->
            <div class="Titulo_Menu">
                <h3 class="Titulo_Lateral">Vuetify Todo List</h3>    
                <span class="Subtitulo_Lateral">By Mariana Ramacciotti</span>  
            </div>  

            <!-- Divisor ------------------------------------------------------------------------------------------------------------------->
            <v-divider></v-divider>

            <!-- Lista com itens do Menu ------------------------------------------------------------------------------------------------------------------->
            <v-list dense nav class="Lista_Menu">                

                <v-list-item-group color="#969FC7" opacity="100%" mandatory>

                    <v-list-item v-for="item in items" :key="item.title" :to="item.to" link div >
                            
                                <!-- Icones da lista -->                 
                                <v-list-item-icon>
                                    <v-icon>{{ item.icon }}</v-icon>
                                </v-list-item-icon>
                                                
                                <!-- Textos da Lista -->
                                <v-list-item-content>
                                    <v-list-item-title>{{ item.title }}</v-list-item-title>
                                </v-list-item-content>

                    </v-list-item>

                </v-list-item-group>

            </v-list>

        </v-navigation-drawer>

        <!-- Barra Superior xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
        <v-app-bar flat prominent absolute app color="primary" dark src="./assets/images/Ocean.jpg">

            <!-- Gradiente ---------------------------------------------------------------------------------------------------------->
            <template v-slot:img="{ props }">
                <v-img v-bind="props" gradient="to top right, rgba(100,115,201,.4), rgba(25,32,72,.4)"></v-img>
            </template>

            <!-- Menu | Aplica classe diferente dependendo do tamanho da tela -------------------------------------------------------------------------------------------------------------------->
            <div :class="{'Centralizar': !$vuetify.breakpoint.xs,'Centralizar_Mobile': $vuetify.breakpoint.xs}">

                <!-- Ícone do menu que fecha e abre ....................................................................................-->
                <v-app-bar-nav-icon @click="drawer = !drawer">
                    <v-icon style="font-size:32px">mdi-menu</v-icon>
                </v-app-bar-nav-icon>

                <!-- Título + Data ..................................................................................................................-->
                <div id="Titulo_Container">

                    <!-- Título do Site -->
                    <v-app-bar-title>                
                        <h1 class="Titulo" style="margin-left:15px">Vuetify Todo</h1>                
                    </v-app-bar-title>

                    <!-- Dia atual -->
                    <div class="Data">
                        {{ new Date() | dateFormat('MMMM DD, YYYY') }}
                    </div>

                </div>

                <!-- Espaço que coloca os icones do lado oposto ......................................................................................-->
                <v-spacer></v-spacer>

                <!-- Ícone ................................................................................................................-->
                <v-btn icon href="https://www.linkedin.com/in/marianaramacciotti/" target="_blank">
                    <v-icon style="font-size:32px" >mdi-linkedin</v-icon>
                </v-btn>

                <!-- Ícone ......................................................................................................................-->
                <v-btn icon href="https://github.com/Ramacciotti" target="_blank">
                    <v-icon style="font-size:32px" >mdi-github</v-icon>
                </v-btn>

            </div>

        </v-app-bar>

        <!-- Definir Rotas xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx -->
        <v-main>
            <!-- Importar as rotas -->
            <router-view></router-view>
        </v-main>

    </v-app>

</template>

<!-- Javscript XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX-->
<script>

export default {

    // Variaveis --------------------------------------------------------------------------------------------------------------------------
    data: () => ({

        // Item 1 ............................................................................................................
        drawer: null,
        
        // Criando links para o menu lateral ..........................................................................
        items: [
            { title: "Todo", icon: "mdi-order-bool-ascending-variant", to: "/" },
            { title: "About", icon: "mdi-information-outline", to: "/about" },
        ],

        // Checar se está no Mobile ................................................................................................
        isMobile: false

    }),

    breakpoint: {
        thresholds: {
            xs: 340,
            sm: 540,
            md: 800,
            lg: 1280,
        },
        scrollBarWidth: 24,
    },
    
};

</script>

<!-- Css XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX-->
<style lang="scss" scoped>
   
    .Centralizar {
        width: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        align-content: center;
        margin-top:35px;
    }
    

    .Centralizar_Mobile {
        width: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        align-content: center;
        margin-top:24px;
    }

    .Centralizar_Mobile h1 {
        font-size: 1.1em;
        margin-bottom:-5px;
    }

    #Titulo_Container {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
    }

    .Titulo{
        font-size: 1.3em;
    }
    
    .Titulo_Menu{
        display: flex;
        flex-direction: column;
        align-items: left;
        padding: 20px 0;
        padding-left: 18px;
    }    

    .Titulo_Lateral {
        color: #6f6e77;
        font-size: 1.6em;
    }

    .Subtitulo_Lateral {
        margin-top:-3px;
        color: #9c9c9c;
    }

    .Data {
        font-size: 17px;
        margin-left: 15px;
        color: white;
    }

</style>

<!-- Global Css XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX-->
<style src="./assets/scss/_global.scss" lang="scss">



</style>