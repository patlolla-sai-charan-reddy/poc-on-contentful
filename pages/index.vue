<template>
  <div class="homePage">
   <!-- <img class="image"  :src="person.fields.background.fields.file.url"> -->
  <div class="home-container">
    <div class="row">
      <div class="col-lg-2">
        <img class="logo" :src="person.fields.fitchLogo.fields.file.url">
      </div>
      <div class="col-lg-10">
        <ul class="row navBar">
          <li class="">
            {{ person.fields.mainMenu }}
          </li>
          &nbsp;
          &nbsp;
          <span>|</span>
          <li class="col-lg-2">
            {{ person.fields.search }}
          </li>
        </ul>
      </div>
    </div>
    <div class="col-lg-9 col-md-9 midContainer">
      <div class="globalSovereign col-lg-9">
        <h1>{{ person.fields.headingMessage }}</h1>
      </div>
      <div class="welcomeMessage col-lg-5">
        <p>{{ person.fields.welcomeMessage }}</p>

        <button class="btn btn-default schedule text-center">
          {{ person.fields.schedule }}
        </button>
      </div>
    </div>

  </div>
    <div class="row section-affirmed">
      <div class=" col-lg-4 sec-1">
        <p>{{ person.fields.welcomeMessage }}</p>
      </div>
      <div class=" col-lg-4 sec-2">
        <p>{{ person.fields.welcomeMessage }}</p>
      </div>
      <div class=" col-lg-4 sec-3">
        <p>{{ person.fields.welcomeMessage }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

import {createClient} from '~/plugins/contentful.js'
import Navigation from '~/components/navigation.vue'
import ArticlePreview from '~/components/article-preview.vue'

const client = createClient()

export default {
  asyncData ({env}) {
    console.log(env)
    return Promise.all([
      client.getEntries({
        'sys.id': env.CTF_PERSON_ID
      }),
      client.getEntries({
        'content_type': env.CTF_BLOG_POST_TYPE_ID,
        order: '-sys.createdAt'
      })
    ]).then(([entries, posts]) => {
      console.log(posts)
      return {
        person: entries.items[0],
        posts: posts.items
      }
    }).catch(console.error)
  },
  components: {
    Navigation,
    ArticlePreview
  }
}
</script>

<style>

/* Landing Page CSS */

.home-container {
  height: 750px;
  margin-left: 25px;
}

.landingPage {
  margin-top: 20px;
}

.logo {
  height: 51px;
}

.menuItems {
  margin-top: 10px;
  color:#FFF;
  letter-spacing: 0.2ex;
}

.globalSovereign {
  padding: 15px;
  background: #fff;
  box-shadow: 0.5px 0.5px 0.5px 0.5px lavenderblush;
  font-size: 25px;
  font-weight: bold;
}

.welcomeMessage {
  margin-top: 15px;
  padding-left:45px;
}

.schedule {
  color: #D44444;
  background: #fff;
  width: 150px;
  border-radius: 15%;
  font-weight: bold;
  margin-top: 20px;
  letter-spacing: 0.2ex;
  padding: 8px;
}

.image {
  height: 100px;
}

.image {
  position: absolute;
}
.section-affirmed {
  padding: 30px;
  background: #2D6480;
  color: #fff;
}

.navBar {
  float:right;
  margin-right: 50px;
}

.homePage {
  width: 1334px;
}

.midContainer {
  margin-top: 50px;
}
/* End of Landing Page CSS */
</style>
