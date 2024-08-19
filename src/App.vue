<script setup lang="ts">
import Collapsible from './components/Collapsible.vue'
import CollapsibleAlt from './components/CollapsibleAlt.vue'

const faqs = [
  {
    title: '1. What products and services do you offer?',
    content:
      'We offer innovative tech gadgets like the QuantumPad tablet and QuirkBot AI assistant, along with smart home solutions like the QuantumLink hub. We also provide AI consulting services for businesses.'
  },
  {
    title: '2. How can I get technical support?',
    content:
      'Visit our website for troubleshooting guides and contact support via live chat, email, or phone. We’re available 24/7 to assist you.'
  },
  {
    title: '3. Is there a warranty on your products?',
    content:
      'Yes, we provide a one-year limited warranty on all products. This covers manufacturing defects but not damage from misuse. Extended warranty options are also available.'
  }
]

const actions = [
  { key: 'a', title: 'Generic A Title', label: 'Another randet content goes in here' },
  { key: 'b', title: 'Generic B Title', label: 'Some random text comes in here' }
]

const items = [
  { key: 'a', title: 'A Title' },
  { key: 'b', title: 'B Title' }
]
</script>

<template>
  <main>
    <!-- SINGLE USER -->
    <Collapsible
      title="Lorem ipsum dolor sit amet."
      content="Lorem ipsum dolor sit amet consectetur adipisicing elit. Atque soluta veniam mollitia eaque facilis. Ex, culpa, praesentium est aspernatur deserunt odio unde quis nostrum corrupti aut explicabo, quia itaque nemo tempore dolores? Distinctio praesentium, iste possimus a fuga id delectus modi recusandae cumque, hic repellendus itaque voluptate necessitatibus? Nostrum, illum."
    />

    <!-- USE WITH AN ARRAY -->
    <Collapsible
      v-for="(faq, index) in faqs"
      :key="index"
      :title="faq.title"
      :content="faq.content"
    />

    <!-- USAGE AS A GENERIC COMPONENT WITH SLOTS -->
    <Collapsible>
      <template #header="{ toggleActive }">
        <div @click="toggleActive">Hello world</div>
      </template>
      <template #content>
        <div class="body">
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Ullam sequi inventore cum, eius
          vero explicabo deleniti fugiat? Possimus atque numquam fugiat, ab quibusdam officiis,
          aperiam dignissimos voluptate porro minus, hic exercitationem molestiae ex! Assumenda
          incidunt eum quod doloremque ea minima molestias earum saepe? Consequatur sed debitis
          omnis velit dolorum fugit, similique odit facere quam accusantium numquam atque ex dolorem
          aut esse sit totam, soluta quos? Voluptatibus, sed accusantium! Iusto dicta nisi officiis
          dignissimos harum tempore ipsam cum doloribus. Ullam corrupti aut porro sunt nobis modi
          veniam quasi sint sapiente! Minus sequi eligendi qui voluptas atque eos natus blanditiis
          enim magnam.
        </div>
      </template>
    </Collapsible>

    <!-- USAGE WITH AN ARRAY AS GENERIC COMPONENT WITH SLOT -->
    <Collapsible v-for="action in actions" :key="action.key">
      <template #header="{ toggleActive }">
        <div @click="toggleActive">
          <h3>{{ action.title }}</h3>
          <p>{{ action.label }}</p>
        </div>
      </template>
      <template #content>
        <div v-if="action.key === 'a'">
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Repudiandae consequuntur
          delectus facilis corrupti voluptate reiciendis quae aut exercitationem quod? Harum.
        </div>
        <div v-if="action.key === 'b'">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Cumque voluptatum quam distinctio
          repudiandae molestiae necessitatibus expedita? Quod officiis dignissimos provident.
        </div>
      </template>
    </Collapsible>

    <!-- USAGE WITH AN ARRAY AS GENERIC COMPONENT, PASSING DYNAMIC SLOTS BASED ON ITEM KEYS -->
    <CollapsibleAlt :items="items">
      <template #a>
        <div>
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Repudiandae consequuntur
          delectus facilis corrupti voluptate reiciendis quae aut exercitationem quod? Harum.
        </div>
      </template>
      <template #b>
        <div>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Cumque voluptatum quam distinctio
          repudiandae molestiae necessitatibus expedita? Quod officiis dignissimos provident.
        </div>
      </template>
    </CollapsibleAlt>
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  gap: 30px;
}
.body {
  padding: 10px 0;
}
</style>
