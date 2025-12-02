<template>
  <div id="app">
    <div class="card">
      <h1 v-if="loading">Loading...</h1>
      <h1 v-else-if="error">Error: {{ error }}</h1>
      <div v-else-if="data">
        <h1>{{ data.name.charAt(0).toUpperCase() + data.name.slice(1) }}</h1>
        <div class="description">
          <p><strong>ID:</strong> #{{ data.id }}</p>
          <p><strong>Types:</strong>
            <span v-for="typeInfo in data.types" :key="typeInfo.slot">
              {{ typeInfo.type.name.charAt(0).toUpperCase() + typeInfo.type.name.slice(1) }}
              <template v-if="!$last">, </template>
            </span>
          </p>
        </div>
        <img :src="data.sprites.other['official-artwork'].front_default" :alt="data.name"
          style="width: 150px; height: auto; display: block; margin: 0 auto;" />
      </div>
    </div>
    <div class="card">
      <h1>Go Search Your Pokemon's Information</h1>
      <label for="poke-input" style="display:block;padding: 10px;">Please input its name:<input id="poke-input"
          type="text" v-model="pokemonName" style="margin-left: 8px; padding: 6px; width: 180px;"></label>
      <h2><a href="https://wiki.52poke.com/wiki/">Go check out all the data of pokemon</a></h2>
    </div>
  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue'
import usePokemon from '../hooks/usePokemon'
const pokemonName = ref('')
const { data, loading, error } = usePokemon(pokemonName);

</script>
<style scoped>
 /* 基础重置与全局样式 */
 * {
   margin: 0;
   padding: 0;
   box-sizing: border-box;
 }

 body {
   font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica,
     Arial, sans-serif;
   background-color: #acc8e5;
   color: #112a46;
   line-height: 1.6;
   padding: 2rem 1rem;
 }

 /* 卡片容器 */
 .card {
   max-width: 600px;
   margin: 2rem auto;
   background: white;
   border-radius: 12px;
   box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
   padding: 2rem;
 }

 /* 标题 */
 h1 {
   font-size: 1.8rem;
   font-weight: 700;
   color: #2c3e50;
   margin-bottom: 1.25rem;
   line-height: 1.3;
 }

 /* 描述段落（用 div 包裹文本） */
 .description {
   font-size: 1rem;
   color: #555;
   margin-bottom: 1.5rem;
 }

 /* 列表样式 */
 ul {
   list-style: none;
   padding-left: 0;
 }

 li {
   padding: 0.5rem 0;
   font-size: 1rem;
   color: #444;
   display: flex;
 }

 li::before {
   content: "•";
   color: #3498db;
   font-weight: bold;
   display: inline-block;
   width: 1.2em;
   font-size: 1.4rem;
   line-height: 1;
   margin-right: 0.5rem;
 }

 /* 响应式优化 */
 @media (max-width: 600px) {
   .card {
     padding: 1.5rem;
   }

   h1 {
     font-size: 1.5rem;
   }
 }
</style>
