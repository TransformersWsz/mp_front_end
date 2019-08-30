<template>
  <div class="app-container documentation-container">
    <div>this phone's phone id is {{ phoneId }}</div>

    <el-row>
      <el-col :xs="24" :sm="24" :md="16" :lg="16" :xl="16">
        <div class="tab-container">
          <el-tabs v-model="activeName" style="margin-top:15px;" type="border-card">

              <el-tab-pane label="规格" name="specification">
                <keep-alive>
                  <tab-pane type="specification" />
                </keep-alive>
              </el-tab-pane>
              
              <el-tab-pane label="指标评分" name="chart">
                <keep-alive>
                  <el-row>
                    <el-col :xs="24" :sm="24" :lg="24">
                      <div class="chart-wrapper">
                        <chart-pane />
                      </div>
                    </el-col>
                  </el-row>
                </keep-alive>
              </el-tab-pane>
            
          </el-tabs>
        </div>
      </el-col>

      <el-col :xs="24" :sm="24" :md="{span: 6, offstet: 2}" :lg="{span: 6, offstet: 2}" :xl="{span: 6, offstet: 2}" class="father" style="margin-top: 50px">
        <div class="t-hover-shadow">
          <el-image src="https://img-blog.csdnimg.cn/20190826161431972.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3RyYW5zZm9ybWVyX1dTWg==,size_16,color_FFFFFF,t_70"></el-image>
        </div>
        <span class="name">OPPO手机</span>
        
      </el-col>
    </el-row>
    
  </div>
</template>

<script>
import tabPane from './components/TabPane'
import chartPane from './components/ChartPane'
export default {
  name: 'Detail',
  components: { tabPane, chartPane },
  data() {
    return {
      phoneId: "",
      activeName: 'chart'
    }
  },
  activated() {
    console.log("active");
    this.getPhoneId();
  },
  mounted() {
    this.getPhoneId();
    console.log("mounted")
  },
  methods: {
    getPhoneId() {
      this.phoneId = this.$route.query.phoneId;
    }
  }
}
</script>

<style lang="scss" scoped>
  .tab-container {
    margin: 30px;
  }

  .father {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .t-hover-shadow {
    background-color:rgba(255, 255, 255, 1);
    transition: transform .3s ease-in-out, box-shadow .3s cubic-bezier(.47, 0, .745, .715), border .3s linear .1s;
  }

  .t-hover-shadow:hover {
    box-shadow: 0 10px 50px rgba(51, 51, 51, .25);
    -webkit-transform: translateY(-10px);
    -moz-transform: translateY(-10px);
    transform: translateY(-10px);
  }

  .name {
    margin-top: 15px;
    font: 700 16px Arial,"microsoft yahei";
    color: #666;
  }


</style>