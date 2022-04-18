<template>
  <div class="mx-10 my-10 m-auto">
    <p v-if="$fetchState.pending"> Loading...</p>
    <p v-else-if="!users"> Users not Found </p>
    <ul v-else class="grid grid-cols-6 gap-4">
      <li class="p-5 col-span-6 md:col-span-3 lg:col-span-2  rounded-lg  border hover:shadow-md " v-for="user in users" :key="user.id">
        <div class="font-medium text-xl">{{user.name}}</div>
        <div class="my-2">
           <span class="font-medium"> Email : {{user.email}}</span><br>
          <span class="text-sm font-medium text-gray-600">{{user.gender.toUpperCase()}}</span>
        </div>
        <span class=" rounded-md px-4 py-1 shadow" :class="user.status === 'active' ? 'bg-green-300' : 'bg-red-300' " >{{user.status}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data(){
    return {
      users:[]
    }
  },
  methods:{
  },

  async fetch(){
      const res = await fetch("https://gorest.co.in/public/v2/users", {
        method:'get',
         headers: {
            'Content-Type':'application/json'
        },
        data:{}
      })
    if (!res.ok) {
      alert('Something is wrong(server)')
    }
    this.users = await res.json()
  }

}
</script>

<style>

</style>
