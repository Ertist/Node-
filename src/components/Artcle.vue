<template>
  <div class="ArticleSection">
    <div class="loading" v-if="loading">
      Loading...
    </div>
    <div class="article" v-else>
      <h1>{{post.title}}</h1>
        <ul>
          <li>·</li>
          <li>·</li>
          <li>·</li>
          <li>·</li>
        </ul>
        <div v-html="post.content" id="content"></div>
    </div>
    <div id="reply">
      <div>
        <div class="replyUp">
          <router-link to=""></router-link>
          <router-link to=""></router-link>
          <span>
            {{}}楼
          </span>
        </div>
        <section>
          <span></span>{{}}
        </section>
        <p></p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Article',
    data() {
      return {
        post: {
          author: {
            loginname: 'temp',// 设置默认值，防止Vue在axios未被调用钱报错
          }
        },
        loading: false
      }
    },
    computed: {
      postTab(){
        var type = this.post.tab.toString();
        if(type = 'ask'){
          return '问答'
        }
        if(type = 'share'){
          return '分享'
        }
        if(type = 'job'){
          return '招聘'
        }
        if(type = 'good'){
          return '精华'
        }
      }
    },
    methods: {
      getData(){
        //获取文章信息
        this.$http({
          url: `https://cnodejs.org/api/v1/topic/${this.$route.params.id}`,  
          //ES6语法，引入组件内的 route object（路由信息对象）
          method: 'get',
          params:{
            mdrender:true
          }
        })
        .then((Response)=> {
          if (Response.data.sucess === true) {
            this.post = response.data.data
            this.loading = false
          }
        })
        .catch(function (error) {
          console.log(error)
        })
      }
    },
    beforeMount() {
      this.loading = true
      this.getData()
    },
    watch: {
      $route(){
        this.getDate()
      }
    }
  }
</script>