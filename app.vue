<template>
  <div class="container" style="padding: 50px 0 100px 0">
    <Account v-if="user" />
    <Auth v-else />
  </div>
</template>

<script setup lang="ts">
  import { Database } from "schema";
  const user = useSupabaseUser()
  const supabase = useSupabaseClient<Database>()

  const hello = await supabase.rpc('hello_world')
  const planet = await supabase.rpc('get_planets').eq('id', 1)

  const { data: todos, error } = await supabase.from('todos').select('*')
  todos?.map((t) => t.task)

  // Listen to inserts
  // const todos = supabase.channel('custom-insert-channel')
  // .on(
  //   'postgres_changes',
  //   { event: 'INSERT', schema: 'public', table: 'todos' },
  //   (payload) => {
  //     console.log('Change received!', payload)
  //   }
  // )
  // .subscribe()

  // const { data, error } = await supabase.functions.invoke('hello-world', {
  //   body: { name: 'Functions' },
  // })
</script>
