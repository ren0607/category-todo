<template>
    <div>
        <v-toolbar dark color="indigo">
            <v-toolbar-title class="white--text">
                MyTodo
            </v-toolbar-title>
        </v-toolbar>

        <v-card v-for="categoryTodos in categorizeTodos"
                v-bind:key="categoryTodos.categoryId"
                class="mx-auto my-12" width="600px">
            <v-card-title>
                {{ categoryTodos['categoryId'] }}
            </v-card-title>
            <v-card-text>
                <v-list>
                    <template v-for="(todo, i) in categoryTodos['todos']">
                        <v-list-item v-bind:key="todo['todoId']">
                            <v-list-item-content>
                                <v-list-item-title>
                                  {{ todo['todo'] }}
                                </v-list-item-title>
                            </v-list-item-content>
                            <v-list-item-action>
                                <v-btn text icon v-on:click="deleteTodo(i)">
                                    <v-icon>delete</v-icon>
                                </v-btn>
                            </v-list-item-action>
                        </v-list-item>
                        <v-divider v-bind:key="`second-${i}`"></v-divider>
                    </template>
                </v-list>
            </v-card-text>
        </v-card>

        <v-btn fab fixed bottom right color="indigo" v-on:click="addTodo">
            <v-icon color="white">add</v-icon>
        </v-btn>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                todos: [],
                categorizeTodos: [],
                category: ['ご飯', '勉強'],
            }
        },
        created() {
            this.todos = JSON.parse(localStorage.getItem('todos')) || [];
            this.categorizeTodos = []
            let id = 0
            for(let i=0; i<this.category.length; i++){
                let temp = [];
                for(let j=0; j<this.todos.length; j++){
                    if(this.category[i] == this.todos[j]['category']){
                        temp.push({todoId:id, todo:this.todos[j]['todo']});
                        id = id+1;
                        // console.log(this.todos[j])
                    }
                }
                this.categorizeTodos.push({categoryId:this.category[i], todos:temp});
            }
            console.log(this.categorizeTodos[1]);
            let a = [[{c:1,b:2},{c:3,b:4}],[{c:5,b:6},{c:7,b:8}]]
            a.push([{c:9,b:10},{c:11,b:12}]);
            // console.log(a)
        },
        computed: {

        },
        methods: {
            deleteTodo(i) {
                this.todos.splice(i, 1);
                localStorage.setItem('todos', JSON.stringify(this.todos));
            },
            addTodo() {
                this.$router.push('/todos/add');
            }
        }
    }
</script>

<style scoped>


</style>
