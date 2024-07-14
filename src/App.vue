<script setup>
  import { ref, computed } from "vue";
  let me = ref({});
  let actualMenu = ref(0);
  let menu = [
    `Sobre mim`,
    `Acadêmico`,
    `Profissional`,
    `Contatos`
  ]
  // Métodos
  let changeMenu = (menuIndex) => actualMenu.value = menuIndex;


  //Propiedades compuatadas
  const titlePage = computed(() =>menu[actualMenu.value]);

  //Ciclo created
  fetch('src/assets/aboutme.json')
  .then(res => res.json())
  .then(data => me.value = data);

</script> 

<template>
  <div class="layout">
    <header >
      <a v-for='(item, index) in menu'
        :key="'menuitem' + index"
        @click = "changeMenu(index)"> 
        {{ item }}
      </a>
     

    </header>

    <main>


      <section v-show = 'actualMenu === 0'>
        <div class="introduction">
          <H2>{{ titlePage }}</H2>
        </div> 
        <div class="wrapper">
          <div class = greetings>
            <p class="title">{{ me.name }}</p>
            <p class="description">{{ me.description }}</p>
          </div>
        </div>
      </section>

      <section v-show = 'actualMenu === 1'>
        <div class="introduction">
          <H2>{{ titlePage }}</H2>
        </div>
        <div class="wrapper">
          <div>
            <div class = item v-for="(item, index) in me.academic" :key = "'academic' + index">
              <p class="title">{{ item.institution }}</p>
              <p class="description">{{ item.course }} {{ item.year }}</p>
            </div>
          </div>
        </div>
      </section>

      <section v-show = 'actualMenu === 2'>
        <div class="introduction">
          <H2>{{ titlePage }}</H2>
        </div>
        <div class="wrapper">
          <div>
            <div class = item v-for="(item, index) in me.professional" :key = "'professional' + index">
              <p class="title">{{ item.company }}</p>
              <p class="description">{{ item.occupation }} - {{ item.period }}</p>
            </div>
          </div>
        </div>
      </section>

      <section v-show = 'actualMenu === 3'>
        <div class="introduction">
          <H2>{{ titlePage }}</H2>
        </div>
        <div class="wrapper">
          <div>
            <div class = item v-for="(item, index) in me.contacts" :key = "'contacts' + index">
              <p class="title">{{ item.text }}</p>
              <p class="description">{{ item.contact }}</p>
            </div>
          </div>
        </div>
      </section>

    </main>

  </div>
</template>

<style scoped>
header{
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
}
a{
  margin: 0 10px;
}
.title{
  height: 50px;
  padding: 15px;
  font-size: 1.5em;
  font-weight: bold;
}
main{
  display: flex;
  justify-content: center;
} 
.title{
  text-align: center;
  padding: 10px;
  margin: 10px 0;
}
.item{
  background-color: rgb(240, 240, 240);
  margin: 10px 0;
  display: flex;
  flex-direction: column;
  border-style: ridge;
}
.introduction{
  font-size: 1.8em;
  font-weight: bold;
  text-align: center
}

</style>
