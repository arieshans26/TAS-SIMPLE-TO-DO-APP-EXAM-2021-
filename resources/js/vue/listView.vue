<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item
            :item="item"
            class="item"
            v-on:itemchanged="$emit('reloadlist')"
            />
            <p id="dateCreated">Date: {{currentDate()}}</p>
        </div>
    </div>
</template>

<script>
import listItem from "./listItem"

export default {
    props: ['items'],
    components: {
        listItem
        
    } ,
    
methods:{
    currentDate() {
      const current = new Date();
      const date = `${current.getDate()}/${current.getMonth()+1}/${current.getFullYear()}`;
      return date;
    }
}
}

</script>

<style scoped>
.item{
    background: #e6e6e6;
    padding: 5px;
    margin-top: 5px;
}
#dateCreated{
    font-size: 12px;
    font-weight: bold;
    color: #0000FF;
    margin: auto;
    background: #e6e6e6;
    padding-left: 45px;
       
}
</style>