<script setup>
import {onUnmounted, ref} from 'vue'
import useChat from '../composable/useChat'
import useAuth from '../composable/useAuth'

const {messages, unsubscribe, sendMessage} = useChat()
const {user} = useAuth()
const newMessage = ref('')

const send = () => {
  sendMessage(newMessage.value)
  newMessage.value = ''
}

onUnmounted(() => {
  unsubscribe()
})
</script>

<template>
  <h1 class="mt-8 text-6xl font-thin tracking-tighter text-center">The Chat Room</h1>
  <div class="min-h-[500px] w-full mt-8 rounded-lg shadow-2xl flex flex-col justify-between">
    <ul class="p-4 space-y-4 ">
      <li v-for="message in messages" :key="message.id" > 
       <div class="flex justify-between px-4 py-2 rounded-lg" 
       :class="user===message.author ?'bg-yellow-300' : 'bg-yellow-200'">
         <span>{{message.text}}</span>
         <span>{{message.author}}</span>
       </div>
       </li>
    </ul>
  <div>
    <input class="w-full p-4 rounded-lg focus:outline-none focus:bg-purple-300"
     type="text" 
     placeholder="Type a message ..."
     v-model="newMessage"
     @change="send"
     />
  </div>
  </div>

  <div class="text-yellow-100 bg-yellow-400">
     <div class="container flex items-center justify-between mx-auto">
        
        <nav>
        <ul class="flex space-x-4">
        
        <router-link :to="{ name: 'About' }">
            <li
              class="px-4 py-8 hover:cursor-pointer hover:bg-yellow-300 hover:text-yellow-500"
            >
              About
            </li>
          </router-link>

          <router-link :to="{ name: 'Contact' }">
            <li
              class="px-4 py-8 hover:cursor-pointer hover:bg-yellow-300 hover:text-yellow-500"
            >
              Contact
            </li>
          </router-link>

          <router-link :to="{name: 'Chat' }">
            <li class="px-4 py-8 hover:cursor-pointer hover:bg-yellow-300 hover:text-yellow-500">Chat With Us</li>
          </router-link>
          </ul>
          </nav>
     </div>
     <h5 class="text-center">2022 © QuiverPoint supply, Inc. All Rights Reserved.</h5>
   </div>
</template>