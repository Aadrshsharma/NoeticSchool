<template>
    <div class="w-full bg-center bg-no-repeat bg-cover h-screen" style="background-color: #F1F1F1">
    <div class="flex h-full w-full" >
        <div class="m-auto">
        <h3 class="text-center text-lg font-bold mb-5">Login</h3>
            <div class="rounded shadow-lg p-6 bg-gray-50" style="width: 440px;">
              <form class="h-full">
                  <div >
                    <div>
                      <label>name </label><br/>
                           <input v-model="name"  class="w-full rounded " type="text"  placeholder="enter your name ">
                    </div>
                    <div class="mt-1">
                      <label  >password</label><br/>
                      <input  v-model="password" class="w-full rounded" type="text" placeholder="enter your password" >
                    </div>
                     <div class="mt-1">
                      <label  >select optionHobbies</label><br/>
                       <div>
                      <Multiselect
                                v-model="multiselect_example"
                                :options="options"
                                mode="tags"
                                
                       />
                     </div>
                    </div>
                  
                   

 
                    <div class="mt-1 text-center ">
                      <label>  </label> <br/>
                        <button @click.prevent="submit" class=" bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded ">Submit</button>
                    </div>
                  </div>
              </form>
            </div>
        </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
 import Multiselect from '@vueform/multiselect'
 export default {
  components: { Multiselect },
    name:"create",
    data(){
        return{
            name:'',
            password:'',
            multiselect_example:[],
            tags:'tags',
            options: [
            { value: 'batman', label: 'Batman' },
            { value: 'robin', label: 'Robin' },
            { value: 'joker', label: 'Joker' },
           ]
        }
        
        },
        methods:{
            submit(){
                const payload = {
                    name:this.name,
                    password:this.password
                }
                axios.post('/api/noetic/create',payload).then(response =>{
                    if(response.status === 200){
                        this.$inertia.get('/view');
                    }
                })
            }
        }
}
</script>
<style src="@vueform/multiselect/themes/default.css"></style>