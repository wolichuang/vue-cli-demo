<template>
    <div class="Demo">
        <h1>按需加载路由</h1>
        <!-- 循环事件绑定 -->
        <ul @click="handleClick">
            <li v-for="(item, index) in lists" :key="index" :data-name="item.name">{{ item.name }}</li>
        </ul>
        <!-- 组件懒加载 -->
        <div>
            <component v-bind:is='page'></component>
            <el-divider></el-divider>
            <button @click="handleLoad">按需加载组件</button>
        </div>
    </div>
</template>
<script>
// const FirstComFirst = () => import('../components/FirstComFirst')
// const FirstComSecond = () => import('../components/FirstComSecond')
// const FirstComThird = () => import('../components/FirstComThird')
export default {
    name: 'Demo',
    data() {
        return {
            lists: [
                {
                    id: 1,
                    name: '苹果'
                }, {
                    id: 2,
                    name: '香蕉'
                }, {
                    id: 3,
                    name: '西红柿'
                }, {
                    id: 4,
                    name: '橙子'
                }, {
                    id: 5,
                    name: '黄瓜'
                }
            ],
            page: () => import('../components/FirstComFirst')
        }
    },
    methods: {
        handleClick(event) {
            const target = event.target;
            const name = target.getAttribute('data-name');
            console.log(name);
        },
        handleLoad() {
            const component = ['FirstComFirst', 'FirstComSecond', 'FirstComThird']
            const name = component[parseInt(Math.random() * component.length, 10)]
            // console.log(`../components/${name}`); // 组件中不能使用 `` 表达式
            this.page = () => import('../components/' + name);
        }
    }
}
</script>
<style>
</style>
