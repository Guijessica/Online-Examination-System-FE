<template>
  <div class="home">
    <TopTab title="首页">
      <div class="tab-content">
        <div class="home-introduce">
          <div>
            <p>欢迎来到OnLine线上考试系统</p>
            <p>这是一款基于前后端分离的线上考试系统</p>
            <p>前端采用vue框架，搭配vue-cli、axios、vuex、element-ui组件库</p>
            <p>后端采用springBoot框架、jwt、swagger、持久层mybatis，mysql数据库</p>
            <p>小组成员：刘杰宜 贺桂金 刘欢 李璇</p>
            <p><a href="https://gitee.com/">https://gitee.com/</a></p>
          </div>
        </div>

        <ul class="home-header">
          <li @click="me">个人资料</li>
          <template v-if="$role('student')">
            <li @click="myClasses">我的班级</li>
            <li @click="finishTest">我参加过的考试</li>
            <li>功能开发中,敬请期待</li>
          </template>
          <template v-if="$role('teacher')">
            <li @click="createClasses">创建班级</li>
            <li @click="createExam">创建试卷</li>
            <li @click="myClasses">我的班级</li>
          </template>
        </ul>
        <ul class="home-content">
          <li class="myMessage">暂无消息通知</li>
          <li class="more">功能开发中,敬请期待</li>
        </ul>
      </div>
    </TopTab>


    <!-- 创建班级对话框 -->
    <CreateClasses ref="createClasses" @success="getClasses()" />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import TopTab from "../../components/TopTab.vue";
import "../../assets/less/main/home.less";
import { mapMutations } from "vuex";
import CreateClasses from '@/views/classes/components/CreateClasses.vue'

export default {
  name: "Home",
  components: {TopTab, CreateClasses },
  data() {
    return {
      enterClasses_id: "",
    };
  },
  created() {},
  watch: {},
  methods: {
    ...mapMutations(["setActiveName"]),

    // 个人中心
    me() {
      this.$router.push({
        name: "Me",
      });
      this.setActiveName("Me");
    },
    
    // 我的班级
    myClasses() {
      this.$router.push({
        name: "ClassesList",
      });
      this.setActiveName(["Classes","ClassesList","ClassesSpace"]);
    },

    // 我参加过的考试
    finishTest() {
      this.$router.push({
        name: "MyFinishTest",
      });
      this.setActiveName("MyFinishTest");
    },

    // 创建试卷
    createExam() {
      const { href } = this.$router.resolve({
        name: "createExam",
        params: { type: 'add'}
      });
      window.open(href, "_blank");
    },

    // 创建班级
    createClasses() {
      this.$refs.createClasses.dialog = true  
    },

    
  },
};
</script>
