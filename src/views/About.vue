<template>
    <div>
        <p>{{title}}</p>
        <Child
            v-bind:array='array'
            v-on:create-element='createElem'
         />
         <Slots v-bind:title='title'>
            <template v-slot:first>
                First slot
            </template>   
            <template v-slot:second>
                Second slot
            </template>
            
         </Slots>
    </div>
</template>

<script>
import Child from '@/components/Child'
import Slots from '@/components/Slots'
export default {
    data() {
        return {
            title: 'Hello',
            array: [1,2,3,4],
            newElemNum: 5,
            user: {
                name: 'alex',
                surname: 'Brown'
            }
        }
    },
     components: {
         Child,
         Slots
     },
     methods: {
         createElem() {
             this.array.push(this.newElemNum)
             this.newElemNum++
         }
     }
}
</script>

