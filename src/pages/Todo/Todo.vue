<!-- Html XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX-->
<template>

    <div id="Container">

        <!-- Adicionar Tarefa --------------------------------------------------------------------------------------------------------------------------->
        <div class="Linha_1">
            <v-text-field 
                v-model="Nova_Tarefa" @click:append="Adicionar_Tarefa" @keyup.enter='Adicionar_Tarefa'
                class="pt-10 pb-5 mx-5 custom-placeholer-color" outlined placeholder="Add Task..." append-icon="mdi-plus" hide-details clearable color="#1C64AB">
            </v-text-field> 
        </div>     
        
        <!-- Lista --------------------------------------------------------------------------------------------------------------------------->
        <div class="Linha_2">

            <v-list subheader two-line flat>  

                <!-- Grupo de itens selecionáveis -->
                <v-list-item-group multiple>

                    <!-- Container que carregará todas as tarefas adicionadas ...................................................................................................-->
                    <div v-for="tarefa in tarefas" :key="tarefa.id">

                        <!-- Lista + Item se torna azul SE a tarefa for feita -->
                        <v-list-item @click="Done_Task(tarefa.id)" :class="{ 'Background_Lista' : tarefa.done }">

                            <template v-slot:default>

                                <!-- Checkbox -->
                                <v-list-item-action>
                                    <div class="Checkbox">
                                        <!--<v-checkbox :input-value="tarefa.done" class="Checkbox"></v-checkbox>-->
                                        <loading-checkbox :checked="tarefa.done" borderColor="rgb(186 186 186)" borderRadius="10%" borderWidth="1.8px" checkedBackgroundColor="#1C64AB" checkedBorderColor="transparent" :size="20" :gap="10"></loading-checkbox>
                                    </div>
                                </v-list-item-action>

                                <!-- Título da Tarefa -->
                                <v-list-item-content :class="{'text-decoration-line-through' : tarefa.done}"> 
                                    <v-list-item-title>{{tarefa.title}}</v-list-item-title>
                                </v-list-item-content>

                                <!-- Botão Deletar Tarefa -->
                                <v-list-item-action>
                                    <v-btn @click.stop="Deletar_Tarefa(tarefa.id)" icon><v-icon color="#1C64AB">mdi-delete</v-icon></v-btn>
                                </v-list-item-action>

                            </template>

                        </v-list-item>

                        <!-- Divisor -->
                        <v-divider></v-divider>

                    </div>    

                </v-list-item-group>

            </v-list>
            
        </div>  

        <!-- Alerta --------------------------------------------------------------------------------------------------------------------------->
        <div class="Linha_3" v-if="alerta">  

            <v-slide-y-transition>      

                <!-- Alerta -->   
                <v-alert class="Alerta Background_Alerta">

                    <v-row align="center">

                        <!-- Coluna 1 -->
                        <v-col class="grow">
                            Task Added!
                        </v-col>

                        <!-- Divisor -->
                        <v-spacer></v-spacer>

                        <!-- Coluna 2 -->
                        <v-col class="shrink">
                            <v-btn class="Botao_Alerta" outlined @click="alerta = false">
                                Close
                            </v-btn>
                        </v-col>

                    </v-row>
                </v-alert>

            </v-slide-y-transition>

        </div>

    </div>

</template>

<!-- Javscript XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX-->
<script>

// Importing Component and style
import LoadingCheckbox from 'vue-loading-checkbox';
import 'vue-loading-checkbox/dist/LoadingCheckbox.css';

export default {

    // Nome --------------------------------------------------------------------------------------------------------
    name: "Todo",

    // Variáveis --------------------------------------------------------------------------------------------------------
    data() {
        return {

            // Variável que recebe o nome da nova tarefa a ser adicionada
            Nova_Tarefa: '',

            // Variável Array
            tarefas:[],

            // Variável para o alerta
            alerta: false,
        }
    },

    // Métodos ----------------------------------------------------------------------------------------------------------------------------------------
    methods: {

        // Adicionar Tarefa .................................................................................................................................
        Adicionar_Tarefa(id){

            // Nova variável que guardará os valores adicionados
            let Nova_Tarefa = {
                
                // Gera id baseado na data e horário
                id: Date.now(),
                // Pega o título que foi colocado na var novatarefa
                title: this.Nova_Tarefa,
                // Não foi cumprida ainda
                done: false
            }

            // Colocar a tarefa nova dentro da array de tarefas
            this.tarefas.push(Nova_Tarefa);

            // Limpar Campo
            this.Nova_Tarefa = '';

            // Dizer que o alerta é true
            this.alerta = true;

            // Fazer alerta desaparecer depois de 5 segundos
            /*window.setInterval(() => {
                this.alerta = false;
            }, 3000)   */
        },

        // Riscar a Tarefa ...........................................................................................................................
        Done_Task(id){

            // Pegar a tarefa correta do array de tarefas. Verifica se o id da tarefa riscada é o mesmo que estamos pegando aqui
            // Usar filtro para selecionar a tarefa pelo ID, e não o array todo
            let tarefa = this.tarefas.filter(tarefa => tarefa.id === id) [0];
            
            // Dizer que a tarefa foi feita
            tarefa.done = !tarefa.done;
        },

        // Deletar Tarefa ..........................................................................................................................
        Deletar_Tarefa(id){

            // Pegar as todas as tarefas que NÃO tem aquele id
            this.tarefas = this.tarefas.filter(tarefa => tarefa.id !== id)
        }
        
    },

    // Componentes ----------------------------------------------------------------------------------------------------------------------------------------
    components: {
        LoadingCheckbox // Registering Component
    }
};

</script>

<style src="./style.scss" lang="scss" scoped>

</style>
