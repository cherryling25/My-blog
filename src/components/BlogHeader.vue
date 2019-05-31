<template>
    <nav>
        <ul>
            <li>
                <router-link to="/" exact>博客</router-link>
                <router-link to="/add" exact>写博客</router-link>
                 <!--exact 这样点哪个，哪个就呈现 active 状态-->
            </li>
        </ul>
    </nav>
</template>

<script>
export default {
    name:"blog-header"
}
</script>

<style scoped>
ul{
    list-style: none;
    text-align: center;
    margin: 0;
}

li{
    display: inline-block;
    margin: 0 10px;
}

a{  /*虽然上面我们没有用到 a 标签，但是去检查元素时，可以看到是用了 a 标签的*/
    color: #ffffff;
    text-decoration: none;
    padding: 12px;
    border-radius: 5px;
}
nav{
    background: crimson;
    padding: 30px 0;
    margin-bottom: 40px;
}

.router-link-active{
    background: rgba(255, 255, 255, 0.8);
    color: #444;
}
</style>
