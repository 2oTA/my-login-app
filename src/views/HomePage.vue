<template>
  <v-container class="home-bg" style="width: 100%; margin: 0 auto;">
  <v-container class="py-6 home-bg" style="width: 92%; max-width: 600px; margin: 0 auto;">
    <!-- 用户卡片 -->
    <v-card class="mb-6 px-4 pt-4 pb-4 card-shadow" elevation="6" style="background: #ffffff; border-radius: 15px;">
      <v-row align="center" justify="space-between">
        <v-row align="center" no-gutters>
          <v-avatar size="36">
            <v-img src="https://cdn-icons-png.flaticon.com/512/3135/3135715.png" />
          </v-avatar>
          <div class="ml-3">
            <div class="text-body-1 font-weight-bold">{{ name || '参赛选手' }}</div>
            <div class="text-caption text-grey-darken-1">用户名:{{ username || '未登录' }}</div>
          </div>
        </v-row>
        <v-btn icon variant="text" size="small">
          <v-icon color="#bdbdbd" @click="logout">mdi-logout</v-icon>
        </v-btn>
      </v-row>
    </v-card>

    <!-- 功能卡片区 -->
    <v-row  dense>
    <v-col cols="12" v-for="(item, i) in features" :key="i" class="mb-4 align-center">
      <v-card elevation="6" class="py-6 px-0 d-flex flex-column align-center feature-card card-shadow" :style="'background: #ffffff; border-radius: 18px; cursor:pointer;'" @click="goFeature(item.route)">
        <v-avatar size="48" :style="'background:' + item.bg">
          <v-icon :color="item.color" size="32">{{ item.icon }}</v-icon>
        </v-avatar>
        <div class="mt-3 text-h6 font-weight-bold">{{ item.title }}</div>
        <div class="mt-1 text-body-2 text-grey-darken-1">{{ item.desc }}</div>
      </v-card>
    </v-col>
    </v-row>
  </v-container>
  </v-container>
</template>

<script setup>
function logout() {
  localStorage.removeItem('participant');
  router.push('/login');
}
import { useRouter } from 'vue-router';
import { ref, onMounted } from 'vue';
const router = useRouter();

const name = ref('');
const username = ref('');

onMounted(() => {
  const user = JSON.parse(localStorage.getItem('participant'));
  if (user) {
    name.value = user.name;
    username.value = user.username;
  } else {
    router.push('/login');
  }
});


const features = [
  {
    icon: 'mdi-account-check',
    color: '#3b82f6',
    bg: '#e8f1ff',
    title: '签到功能',
    desc: '比赛签到，记录参赛信息',
    route: '/signin'
  },
  {
    icon: 'mdi-file-document-outline',
    color: '#34c759',
    bg: '#e8fbe8',
    title: '查看报告',
    desc: '成绩报告的查看与下载',
    route: '/report'
  },
  {
    icon: 'mdi-gavel',
    color: '#ff9800',
    bg: '#fff7e6',
    title: '申诉功能',
    desc: '提交成绩争议申诉',
    route: '/appeal'
  },
  {
    icon: 'mdi-video',
    color: '#a259ff',
    bg: '#f5e8ff',
    title: '比赛录像',
    desc: '查看录像回放',
    route: '/video'
  }
]

function goFeature(route) {
  if (route) router.push(route);
}
</script>

<style scoped>
.text-h6 {
  font-size: 1.15rem;
}

.v-card {
  box-shadow: none;
}

.card-shadow {
  box-shadow: 0 2px 8px #e3e8f7 !important;
}

.home-bg {
  background: #f5f7ff;
  min-height: 100vh;
  padding: 0;
}

body, html, #app, .v-application {
  background: #f5f7ff ;
}

</style>
