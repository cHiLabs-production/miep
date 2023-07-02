<script setup lang="ts">
import { ref } from 'vue'

const val = ref('')
const s = ref('')

const emotelist:any = ref([])

function parse () {
  const file = JSON.parse(val.value)
  emotelist.value = file
  alert('success.')
}

function search () {
  parse()
  emotelist.value = emotelist.value.filter((e: any) => {
    return e.title.toString().indexOf(s.value) !== -1
  })
}

function store () {
  localStorage.setItem("emote", val.value)
  alert('success.')
}

function get () {
  //@ts-ignore
  val.value = localStorage.getItem("emote")
  parse()
}

function clean () {
  localStorage.setItem("emote", "")
  alert('success.')
}

</script>

<template>
  <div id="container">
    <h1>Yet Another Emote Parser</h1>
    <textarea placeholder="paste the json file here." style="width: 100%;" v-model="val"></textarea>
    <input placeholder="search:" v-model="s"/> <button @click="search">Search</button><button @click="parse">Parse</button><button @click="store">Store to localstorage</button><button @click="get">Get from localstorage</button><button @click="clean">Clean Data</button>
    <hr/>
    <h2>{{ emotelist.length }} Emotes</h2>
    <div style="display: flex;flex-wrap: wrap;">
      <div v-for="i in emotelist" style="padding: 2px; border: 1px soild black;">
        <div :title="i.url" >{{ i.title }}</div>
        <div>{{ i.name }}</div>
        <img :src="i.url" style="width:128px;height:128px"/>
      </div>
    </div>
    <hr/>
    <h2>Usage: Emotes from miyoushe(https://miyoushe.com/)</h2>
    <h2>Howto: Copy the elements from emote table(inspect in devtools) the class name must be "mhy-emoticon__list"  , copy it by right click "Edit as HTML attrible" into your computer. Create a html file and Add these under this:</h2>
    <img src="@/assets/pic1.png" style="width: 50%;"/>
    <pre>
      &lt;div id="b"&gt;&lt;/div&gt;
      &lt;script&gt;
        let a = []
        for(i in document.getElementsByClassName("mhy-emoticon__list")[0].childNodes) {
        pic = (document.getElementsByClassName("mhy-emoticon__list")[0].childNodes[i].style?.backgroundImage)
        if (pic) {
          a.push({ 
            url: pic.toString().slice(5,-2),
            title: document.getElementsByClassName("mhy-emoticon__list")[0].childNodes[i].title,
            character: document.getElementsByClassName("mhy-emoticon__list")[0].childNodes[i].title.toString().split('-')[0]
          })
        }
        // for(i in document.getElementsByClassName("mhy-emoticon__list")[1].childNodes) {
        // pic = (document.getElementsByClassName("mhy-emoticon__list")[1].childNodes[i].style?.backgroundImage)
        // if (pic) {
          document.getElementById("b").innerHTML = JSON.stringify(a)
        // }
      }
      &lt;/script&gt;
    </pre>
    <h2>Then, Open the html file with your Browser, copy the result (Ctrl + A, Ctrl + C), then paste it to this page. Enjoy it!</h2>
    <hr/>
    <h3>Made by chihuo2104. Engined by vue. cHiLabs Production&copy;2018-2023.</h3>
  </div>
</template>

<style>
html {
  font-family: "California", Arial, Helvetica, sans-serif;
}
</style>
