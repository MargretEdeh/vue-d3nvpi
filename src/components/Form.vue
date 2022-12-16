<template>
    <div class="form">
<form @submit="addTodo" class="input-form">
    <input class="input" type="text" placeholder="Title" v-model="title">
    <input class="input" type="text" placeholder="Sub Title" v-model="subTitle">
    <textarea  class="text" placeholder="Description" v-model="description"></textarea>
    <input class="btn1" type="submit" value=" + Add"/>
</form>

    </div>
</template>
<script>
export default {
    name: 'FormPart',
    props:{
        method:{
            type: Function,
            }
    },
    data(){
        return{
            title: '',
            subTitle: '',
            description: '',
            isChecked: false,
            // addTodos: [
            //     {
            //         title: 'Title',
            //         subTitle: 'Sub Title',
            //         description: 'Description'
            //     }
            // ]
        }
        
    },
    methods:{
        
        addTodo(e){
            e.preventDefault()
            if (this.title === '' || this.subTitle === '' || this.description === ''){
                alert('Please fill all fields')
                return
            }
            const theTodo = {
                title: this.title,
                subTitle: this.subTitle,
                description: this.description,
                isChecked: false,

            }
            this.$emit('add-todos', theTodo )
            // console.log(this.theTodo)
            
            this.title = ''
            this.subTitle = ''
            this.description = ''
            this.isChecked=" "
            this.method()

        }
    }
}
</script>
<style scoped>
.input{
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: none;
    border-bottom: 1px solid #e83a64;
    outline: none;
    font-size: 20px;
    font-weight: 600;
    color: #161616;
    font-style: oblique;

}
.form{
    width: 100%;
}
.input-form{
    display: flex;
    flex-direction: column;
    width: 80%;
    align-items: center;
    justify-content: center;
    /* margin-left: 20px; */
    margin: 0 auto;
}
.text{
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: none;
    background-color: #f5dbcc;
    border-radius: 10px;
    /* box-shadow: 0px 1px 3px 0.5px #1f1e1e; */
    /* border-bottom: 1px solid #e83a64; */
    font-style: oblique;
    outline: none;
    font-size: 20px;
    font-weight: 600;
    color: #161616;
    height: 150px;
}
.btn1{
    width: 100%;
    font-style: oblique;
    padding: 12px;
    font-weight: 600;
    color: white;
    outline: none;
    border-radius: 10px;
    border: none;
    background-color: #fd995e;
    /* background-color: #e83a64 ; */
}
</style>