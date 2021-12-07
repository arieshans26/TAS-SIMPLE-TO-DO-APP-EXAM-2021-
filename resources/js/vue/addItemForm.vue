<template>
    <div class="addItem">
        <input type="text" v-model="item.task"/>
        
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[ item.task ? 'active' : 'inactive', 'plus']"
            
        />
        
    </div>
</template>

<script>
export default {
    props: ['items'],
    data: function (){
        return {
            item:{
                task: ""
            },
            tasks: []
            
        }
    },
    
    methods:{     
        checkItem(){
            
            //this block retrieve all data from the item table
           
            //compare inputs from database.
            //If the inputs already exist. show notif
            
             

            //if not call addItem()
        },
       
        addItem (){

             axios.get('api/items')
            .then( response => {
                this.tasks = response.data
                console.log(this.tasks);

            })
            if(!this.item.task.includes(this.tasks)){
                console.log(this.item.task.includes(this.tasks));
                Swal.fire({
                icon: 'Warning!',
                title: 'Duplicate task!',
                text: 'Please enter another task.',
                })
                return;
            }

            if( this.item.task == ''){
                return;
            }
                axios.post('api/item/store', {
                item: this.item
                   
                })
                
            
            .then( response =>{
                if( response.status == 201){
                    this.item.task = "";
                    this.$emit('reloadlist');
                   
                     
                    
                }
                
            })
           
            
            .catch( error =>{
                console.log(error);
            })
            //for if
        }
    }
}
</script>


<style scoped>
.addItem{
    display: flex;
    justify-content: center;
    align-items: center;
}

input{
    background: #f7f7f7;
    border: 0px;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}
.plus {
    font-size: 20px;
}
.active {
    color: #00CE25;
}
.inactive{
    color: #999999
}
</style>