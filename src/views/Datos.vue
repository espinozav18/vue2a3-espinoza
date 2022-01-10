<template>
  <div class="home">
    <Suspense>
   <template #default>
        <HelloWorld msg=""/>
   </template>
   <template #fallback>
       Cargando...
   </template>
</Suspense>
   
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Datos',
  components: {
    HelloWorld
  }
}
</script>
