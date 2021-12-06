<template>
  <div class="bg-gray-100 rounded shadow flex items-center justify-between p-2">
        <p v-if="!props.done" class="font-semibold">{{props.title}}</p>
        <del v-else class="font-semibold">{{props.title}}</del>
        <div>
            <button @click="isDone" class="bg-blue-500 shadow-md hover:bg-blue-700 rounded p-1 text-white font-semibold mr-1">Done</button>
            <button @click="hapus" class="bg-red-500 shadow-md hover:bg-red-700 rounded p-1 text-white font-semibold">Hapus</button>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        title:{
            type: String,
            default: ""
        },
        done:{
            type: Boolean,
        },
        id:{
            type: Number,
            default: null
        }
    },
    setup(props, {emit}){
        const hapus = ()=>{
            emit("hapus", props.id)
        }
        const isDone = ()=>{
            emit("isDone", {done: true, id: props.id})
        }
        return{
            props,
            hapus,
            isDone
        }
    }
}
</script>