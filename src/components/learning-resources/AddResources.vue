<template>
    <base-dialog @close="confirmError" v-if="inputIsInvalid" title="Invalid Input">
    <template #default>
        <p>at least one input value in invalid.</p>
        <p>please check all inputs and make sure you entered at least a few characters into each input field.</p>
    </template>

    <template #actions>
        <base-button @click="confirmError">Okay</base-button>
    </template>

    </base-dialog>

    <base-card>
    <form @submit.prevent="submitData">

        <div class="form-control">
            <label for="title"> Title</label>
            <input ref="titleInput" id="title" name="title" type="text"/>
        </div>

        <div class="form-control">
            <label for="description"> Description</label>
            <textarea ref="descriptionInput" id="description" rows="3" name="description" type="text"/>
        </div>

        <div class="form-control">
            <label for="link"> Link</label>
            <input ref="linkInput" id="link"  name="link" type="text"/>
        </div>

        <div> 
            <base-button type="submit"> Add Resource</base-button>
        </div>

    </form>
    </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue'
export default {

    components:{BaseButton},
    inject:["addResources"],
    data(){
        return{
            inputIsInvalid:false
        }
    },
    methods:{
        submitData(){
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDes = this.$refs.descriptionInput.value;
            const enteredLink = this.$refs.linkInput.value;
            
            if(enteredTitle.trim() ==='' || enteredDes.trim() ==='' || enteredLink.trim() ==='') {
                this.inputIsInvalid = true;
                return;
            }
            this.addResources(enteredTitle, enteredDes, enteredLink)
        },
        confirmError(){
            this.inputIsInvalid=false;
        }
    }
}
</script>

<style scoped>

label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
  }
  
  input,
  textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
  }
  
  input:focus,
  textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
  }
  
  .form-control {
    margin: 1rem 0;
  }

</style>