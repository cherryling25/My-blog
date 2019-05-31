<template>
  <div v-theme:column="'narrow'" id="show-blogs">
   <h1>博客总览</h1>
   <input type="text" v-model="search" placeholder="搜索">
   <div v-for="blog in filteredBlogs" class="single-blog">
       <router-link v-bind:to="'/blog/' + blog.id">   <!--blog.id 里的blog是上面 for循环里的-->
       <h2 v-rainbow>{{blog.title  | to-uppercase}}</h2>
       </router-link>

       <article>
           {{blog.body | snippet}}
       </article>
   </div>
  </div>
</template>

<script>


export default {
  name: 'show-blogs',
  data(){
      return {
          blogs:[],
          search:""
      }
  },
  created(){
      this.$http.get("./../static/posts.json")
      .then(function(data){
          //console.log(data);
          this.blogs = data.body.slice(0,10);
          //console.log(this.blog);
      })
  },
  computed:{
      filteredBlogs:function(){
          return this.blogs.filter((blog) =>{   //blogs里所有内容，然后过滤blog里，
              return blog.title.match(this.search); // 选择 title 与 search 相匹配的
          })
      }
  },
    filters:{   //局部自定义过滤器
        //"to-uppercase":function(value){
            //return value.toUpperCase();
        //}
        toUppercase(value){//另一种写法，直接用方法形式
            return value.toUpperCase();
        }
    },
       
    directives:{     //局部注册指令
    "rainbow":{
            bind(el,binding,vnode){
                el.style.color="#" + Math.random().toString(16).slice(2,8);
            }
        }
    }
  
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0 auto;
}

.single-blog{
    background: #eee;
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box; 
    border: 1px dotted #aaa;
}

#show-blogs a{
    color: #444;
    text-decoration: none;
}

input[type="text"]{
    padding: 8px;
    width:100%;
    box-sizing: border-box;
}
</style>
