<!--
    @describe：表单 —— 单列
    @Author: zouwf
    @Date: 2020-09-13
-->
<template>
  <main class="frame">
    <el-row :gutter="20">
      <el-col :span="6"
              v-for="(item, index) in data"
              :key="index"
      >
        <div class="frame-box"  @click="handleClickOpenCode(item)">
          <div class="frame-box__header"
               :style="{
               background: `rgba${item.color}`,
               border: `rgba${item.color}`}"
          >
            <img :src="item.imgUrl" alt="/">
          </div>
          <footer>
            <h2>{{index + 1 + "、" +item.title}}</h2>
            <p>{{item.detail}}</p>
          </footer>
        </div>
      </el-col>
    </el-row>
  </main>
</template>

<script>
  export default {
    name: '',
    props: {
      data:{
        type: [Array, Object],
        default(){
          return [
            {
              title: '单列表单',
              detail: '单列表单、带验证、各种配置',
              imgUrl: '',
              code: ''
            },
            {
              title: '双列表单',
              detail: '双列表单、带验证、各种配置',
              imgUrl: '',
              code: ''
            }
          ]
        }
      }
    },

    components: {},

    data () {
      return {}
    },

    // 计算属性
    computed: {},

    // 方法y
    methods: {

      getColor () {
        this.data.forEach((val) => {
          this.$set(val, 'color', this.getRgb())
        })
      },

      /**
       *  生成随机rgba 三个值
       *  @param：{r,g,b} 代表rgba三个颜色
       * */
      getRgb () {
        const r = Math.floor(Math.random() * 256),
          g = Math.floor(Math.random() * 256),
          b = Math.floor(Math.random() * 256);
        return '(' + r + ',' + g + ',' + b + ')'
      },

      /**
       *  打开代码详情
       *  @param：{item} 当前项目数据
       * */
      handleClickOpenCode (item) {
        let routeData = this.$router.resolve({
          name: 'code-details',
          query: {
            code:item.code,
          }
        });
        window.open(window.location.origin + routeData.href)
      }
    },

    created () {
      this.getColor();
    },

    mounted () {
    }
  }
</script>

<style lang="scss" scoped>
  .frame{

    .frame-box{
      width: 100%;
      height: 290px;
      margin-bottom: 20px;
      box-sizing: border-box;
      border-radius: 5px;
      cursor: pointer;
      box-shadow: 0 1px 3px rgba(0,0,0,0.18);

      .frame-box__header{
        width: 100%;
        height: 220px;
        border: 1px solid #86cb87;
        box-sizing: border-box;
        background: #86cb87;
        padding: 15px;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;

        img{
          width: 100%;
          height: 100%;
          border-radius: 5px;
          transition: all .5s;
        }
      }

      .frame-box__header:hover img{
        transform: scale(1.12);
      }

      footer{
        height: calc(100% - 220px);
        padding: 0 10px;
        box-sizing: border-box;
        background: #f6f6f6;
        border: 1px solid #f6f6f6;
        border-bottom-left-radius: 5px;
        border-bottom-right-radius: 5px;

        h2,p{
          overflow: hidden;
          text-overflow:ellipsis;
          white-space: nowrap;
        }

        h2{
          font-size: 14px;
          color: #60BDE8;
          line-height: 1;
        }

        p{
          color: #838383;
        }
      }
    }
  }
</style>
