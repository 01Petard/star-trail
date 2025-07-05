<script setup>
import {onMounted, reactive} from 'vue'
import StarTrails from './components/StarTrails.vue'

const data = reactive({
  titleList: [
    '热爱……',
    '敬畏之心！',
    '赞美之心！',
    '我很好奇！',
    '你好，请多指教',
    '*舒缓的现代音乐*',
    '希望能成为有趣的人',
    '相信美好的事情即将发生',
    '平凡的日常正奇迹的发生着',
    '你所热爱的<br/>就是你的生活',
    '给时光以生命<br/>给岁月以文明',
    '路虽远行则将至<br/>事虽难做则必成',
    '一望无际的迷雾中<br/>有人在寻找光明',
    '当你在凝视着网页的时候<br/>网页也正在凝视着你',
  ],
  navLinks: [{
    name: '博 客',
    link: 'https://01petard.github.io/blog-vue-vitepress/',
  }, {
    name: '留 言',
    link: 'https://01petard.github.io/messageboard/',
  }],

  myProjects: [{
    name: 'RAG知识库应用',
    description: 'AI志愿填报顾问',
    link: 'https://www.codebox.icu:8888/',
  },{
    name: 'Pintree收藏夹',
    description: '配置型个人收藏夹',
    link: 'https://01petard.github.io/Pintree-fav/',
  }, {
    name: '代码港湾',
    description: '个人知识库，学习&随笔',
    link: 'https://01petard.github.io/blog-vue-vitepress/',
  }, {
    name: '花火の红玉宫',
    description: '旧时博客',
    link: 'https://01petard.github.io/',
  }],

  socialLinks: [{
    icon: '<i i-ant-design-user-outlined />',
    link: 'https://www.codebox.icu/',
    label: 'Star-Trail',
  }, {
    icon: '<i i-ant-design-github-outlined />',
    link: 'https://github.com/01Petard/',
    label: 'Github',
  }, {
    icon: '<i i-ant-design-bilibili-outlined />',
    link: 'https://space.bilibili.com/12764212/',
    label: 'Bilibili',
  }],
})

const avatar = 'https://cdn.jsdelivr.net/gh/01Petard/imageURL@main/img/202503221816953.png'

onMounted(() => {
  // 背景固定
  window.addEventListener('scroll', () => {
    const bg = document.getElementById('background')
    const scrollTop = window.scrollY
    if (scrollTop > 0.7 * window.innerHeight)
      bg.classList.add('fixed')
    else
      bg.classList.remove('fixed')
  })
})
</script>

<template>
  <!-- 导航 -->
  <nav absolute fixed bottom-4 left-4 z-20>
    <div v-for="(item, index) in data.navLinks" :key="index" my-6 text-3 text-white wv>
      <a :href="item.link" opacity-75 text-white tracking-widest hover:opacity-100>
        {{ item.name }}
      </a>
    </div>
  </nav>

  <!-- 主体 -->
  <main bg-transparent absolute w-full top-75vh z-10>
    <!-- 大标题 -->
    <section ml-15vw absolute>
      <div text-10 text-white font-bold tracking-widest v-html="data.titleList[Math.floor(Math.random() * data.titleList.length)]"/>
      <div flex items-center>
        <div mr-4 flex gap-2>
          <div bg-red rounded-full h-3 w-3/>
          <div bg-yellow rounded-full h-3 w-3/>
          <div bg-green rounded-full h-3 w-3/>
        </div>
        <div text-4 text-white tracking-widest>
          天天快乐
        </div>
      </div>
    </section>
    <!-- 个人简介 -->
    <section mx-9vw mt-90>
      <!-- 关于我 -->
      <div text-bold mb-4 ml-10 text-8 text-white>
        About Me
      </div>
      <div mx-10 mb-10 flex justify-between>
        <div class="text-white/80">
          <p leading-10>
            嗨，你好，我是小黄同学。热爱编程、数码、游戏。
          </p>
          <p leading-10>
            热爱软件工程和 IT 互联网事业，希望能成为一名优秀的开发者。
          </p>
          <p leading-10>
            热爱计算机科学和 IT 互联网事业，希望能成为一名优秀的开发者。
          </p>
          <p leading-10>
            我们正在让这个世界变得更加美好，通过代码的重复使用和延展构建完美体系。
          </p>
          <p leading-10>
            We're making the world a better place. Through constructing elegant hierarchies for maximum code reuse and extensibility.
          </p>
        </div>
        <img hidden rounded-full h-25 w-25 transition md:block hover:-translate-y--2 :src="avatar" alt="avatar">
      </div>

      <!-- 我的技能 -->
      <!-- <div text-bold mb-2 ml-10 text-8 text-white>
          My Skills
        </div> -->

      <!-- 我的项目 -->
      <div text-bold mb-2 ml-10 text-8 text-white>
        Projects
      </div>
      <div mb-10 flex flex-wrap justify-between>
        <div v-for="(item, index) in data.myProjects" :key="index" mx-10 my-4 class="basis-3/4 md:basis-1/6">
          <a :href="item.link">
            <div class="bg-white/5 hover:bg-white/10" p-2 rounded-lg shadow-md flex-col transition backdrop-blur-3xl backdrop-opacity-60 hover:backdrop-opacity-100 hover:-translate-y-2>
              <div text-bold opacity-75 text-white>
                {{ item.name }}
              </div>
              <div mt-1 opacity-50 text-3 text-white>
                {{ item.description }}
              </div>
            </div>
          </a>
        </div>
      </div>

      <!-- 社交链接 -->
      <div text-bold mb-2 ml-10 text-8 text-white>
        Find Me
      </div>
      <div flex flex-wrap justify-between>
        <div v-for="(item, index) in data.socialLinks" :key="index" mx-10 my-4 class="basis-1/4">
          <a class="bg-white/5 hover:bg-white/10" p-2 rounded-lg shadow-md flex-col justify-between items-center transition backdrop-blur-3xl backdrop-opacity-60 hover:backdrop-opacity-100
             hover:-translate-y-2 :href="item.link">
            <div mb-1 text-white f-c-c v-html="item.icon"/>
            <div text-bold opacity-75 text-white>{{ item.label }}</div>
          </a>
        </div>
      </div>
    </section>

    <!-- 底部 -->
    <footer mb-5>
      <div class="text-white/60" mt-50 f-c-c>
        <i i-ant-design-environment-outlined mr-1/>
        <p>路虽远行则将至，事虽难做则必成</p>
        <i i-ant-design-environment-outlined ml-1/>
      </div>
      <div class="text-white/60" mt-2 f-c-c gap-4>
        <div>
          <a href="https://beian.miit.gov.cn/" style="color: #999999" target="_blank">
            浙ICP备2024084383号
          </a>
        </div>
        <div>
          ©2025 小黄同学
        </div>
      </div>
    </footer>
  </main>

  <!-- 背景 -->
  <div id="background" absolute wh-full left-0 top-0 z-0>
    <!-- 渐变阴影 -->
    <div to-black-500 absolute h-80vh w-full bottom--30vh left-0 from-black bg-gradient-to-t/>
    <!-- 星轨背景 -->
    <StarTrails pb-45vh bg-black/>
  </div>
</template>

<style lang="scss" scoped>
#background.fixed {
  position: fixed;
  top: -70%;
}
</style>
