<template>
  <div class="bg-gray-100 h-screen">
    <p class="text-2xl font-bold text-center p-5">Aplikasi Todo Sederhana</p>
    <div class="bg-white w-max my-0 mx-auto shadow-md rounded-lg">
        <div class="bg-gradient-to-tr from-blue-800 to-blue-500 p-4 rounded-t-lg flex justify-center">
            <input v-model="inputan" class="rounded focus:ring-2 focus:outline-none shadow focus:ring-blue-700 p-1" type="text" />
            <button @click="tambahTodo" class="bg-white hover:bg-gray-300 shadow ml-2 px-2 text-green-600 font-bold rounded py-1">Tambah</button>
        </div>
            <div class="flex flex-col-reverse relative">
                <transition-group
                name="list"
                appear 
                @enter="enter"
                @after-enter="afterEnter"
                @leave="leave"
                >
                <div v-for="item in todo" :key="item.id" class=" px-3 pt-2 transition-all duration-100 ease-linear">
                    <ListTodo
                    :id="item.id" 
                    :title="item.title" 
                    :done="item.done"
                    @hapus="hapusTodo"
                    @isDone="isDoneTodo"
                    />
                </div>
                </transition-group>
            </div>
            <p class="px-3 pb-2 font-semibold transition-all duration-500">Total Todo: {{todo.length}}</p>
    </div>
  </div>
</template>

<script>
import ListTodo from "./components/ListTodo.vue"
import {reactive, ref} from "vue"
export default {
    components:{
        ListTodo
    },
    setup(){
        const todo = reactive([])
        const inputan = ref("")
        const onShow = ref(false)
        const id = ref(0)
        const tambahTodo = ()=>{
            id.value++
            todo.push({id: id.value ,title: inputan.value, done: false})
            inputan.value = ""
        }
        const hapusTodo = (val)=>{
            let removeIndex = todo.map(item => { 
                    return item.id 
                }).indexOf(val);
            todo.splice(removeIndex, 1);
        }
        const isDoneTodo = (val)=>{
            todo[val.index].done = val.done
        }
        const muncul = ()=>{
            onShow.value = !onShow.value
        }

        const enter = (el) => {
            el.style.opacity = "0"
            el.style.scale = "0"
        }

        const afterEnter = (el) => {
            el.style.opacity = "1"
            el.style.scale = "1"
        }

        const leave = (el) =>{
            el.style.opacity = "0"
            el.style.scale = "0"
        }

        return{
            todo,
            inputan,
            tambahTodo,
            hapusTodo,
            isDoneTodo,
            muncul,
            onShow,
            enter,
            afterEnter,
            leave,
        }
    }
};
</script>

<style>

</style>