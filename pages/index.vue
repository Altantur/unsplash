<template>
  <div class="container1">
    <div v-if="showNew || !!toBeDeleted" class="overlay" @click="showNew = false" />
    <div v-if="!!toBeDeleted" class="add-new delete-dialog">
      <div class="title">
        Are you sure?
      </div>
      <div class="flex flex-col">
        <div class="label">
          Password(onetwothreefour)
        </div>
        <input v-model="password" class="text-input" type="password" :class="{'wrong-border': wrong}">
      </div>
      <div class="flex flex-row-reverse">
        <button class="submit delete-button" @click="remove">
          Delete
        </button>
        <button class="cancel" @click="toBeDeleted = 0">
          Cancel
        </button>
      </div>
    </div>
    <div v-if="showNew" class="add-new">
      <div class="title">
        Add a new photo
      </div>
      <div class="flex flex-col">
        <div class="label">
          Label
        </div>
        <input v-model="title" class="text-input" type="text" placeholder="Then, write the code">
      </div>
      <div>
        <div class="label">
          Photo URL
        </div>
        <input v-model="url" class="text-input" type="text" placeholder="https://images.unsplash.com/photo-1593642634443-44adaa06623a?ixid=MXwxMjA3fDF8MHxlZGl0b3JpYWwtZmVlZHwxMXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60">
      </div>
      <div class="flex flex-row-reverse">
        <button class="submit" @click="submit">
          Submit
        </button>
        <button class="cancel" @click="showNew = false">
          Cancel
        </button>
      </div>
    </div>
    <div class="header">
      <div class="left">
        <nuxt-link to="/">
          <div class="logo" />
        </nuxt-link>
        <input v-model="query" class="search" type="text" placeholder="Search by name">
      </div>
      <button class="add-photo" @click="showDialog">
        Add a photo
      </button>
    </div>
    <div class="images">
      <div class="">
        <div v-for="(image, index) in images.filter((el, ind) => (ind + 1) % 3 === 1)" :key="index" class="img">
          <img :src="image.src">
          <div class="delete flex items-center justify-center" @click="toBeDeleted = image.id">
            delete
          </div>
          <div class="title">
            {{ image.title }}
          </div>
        </div>
      </div>
      <div class="">
        <div v-for="(image, index) in images.filter((el, ind) => (ind + 1) % 3 === 2)" :key="index" class="img">
          <img :src="image.src">
          <div class="delete flex items-center justify-center" @click="toBeDeleted = image.id">
            delete
          </div>
          <div class="title">
            {{ image.title }}
          </div>
        </div>
      </div>
      <div class="">
        <div v-for="(image, index) in images.filter((el, ind) => (ind + 1) % 3 === 0)" :key="index" class="img">
          <img :src="image.src">
          <div class="delete flex items-center justify-center" @click="toBeDeleted = image.id">
            delete
          </div>
          <div class="title">
            {{ image.title }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    images: [
      {
        id: 1,
        title: '1. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617105106017-8a99f99e6b14?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxMnx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 2,
        title: '2. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617054175880-d1e4fa753bd3?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHw5fHx8ZW58MHx8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 3,
        title: '3. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617119552123-60b37a5947fc?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHw3fHx8ZW58MHx8fA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 4,
        title: '4. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617103901487-3f2714ec9692?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxM3x8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 5,
        title: '5. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617121361721-618914459dc8?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwxOHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 6,
        title: '6. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617061850908-dce590ba9d92?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwyNnx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 7,
        title: '7. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617115609755-9238e226b860?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwyOXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 8,
        title: '8. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617109646716-a5185a044ded?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwzNXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 9,
        title: '9. Then, write the code',
        src: 'https://images.unsplash.com/photo-1617102654410-94f143860636?ixid=MXwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHwzOHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      },
      {
        id: 10,
        title: '10. Then, write the code',
        src: 'https://images.unsplash.com/photo-1593642634443-44adaa06623a?ixid=MXwxMjA3fDF8MHxlZGl0b3JpYWwtZmVlZHwxMXx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60'
      }
    ],
    showNew: false,
    toBeDeleted: 0,
    password: '',
    url: '',
    wrong: false,
    query: '',
    images_backup: [],
    title: ''
  }),
  watch: {
    query (val) {
      this.search()
    }
  },
  created () {
    this.images_backup = this.images
  },
  methods: {
    search () {
      if (this.query) {
        this.images = this.images_backup.filter(el => el.title.includes(this.query))
      } else {
        this.images = this.images_backup
      }
    },
    remove () {
      if (this.password === '1234') {
        this.images = this.images.filter(el => el.id !== this.toBeDeleted)
        this.images_backup = this.images_backup.filter(el => el.id !== this.toBeDeleted)
        this.toBeDeleted = 0
        this.wrong = false
        this.password = ''
      } else {
        this.wrong = true
      }
    },
    submit () {
      const id = this.images.reduce((latest, curr) => {
        latest = latest < curr.id ? curr.id : latest
        return latest
      }, 0) + 1
      this.images = [{ id, title: this.title, src: this.url }, ...this.images]
      this.images_backup = [{ id, title: this.title, src: this.url }, ...this.images_backup]
      this.showNew = false
    },
    showDialog () {
      this.url = ''
      this.title = ''
      this.showNew = true
    }
  }
}
</script>
