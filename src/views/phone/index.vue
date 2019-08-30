<template>
  <div class="app-container">
    <el-row>
      <el-col :span="4" v-for="(image, index) in imageList" :key="index" :offset="1">
        <el-card :body-style="{ padding: '10px' }" style="margin-bottom: 10px" shadow="hover">
          <el-image :src="image.url"></el-image>
          <div style="padding: 14px;">
            <span>{{image.brand}}</span>
            <div class="bottom clearfix">
              <time class="time">{{ currentDate }}</time>
              <el-button type="text" class="button" @click="jumpToDetail(image.phoneId)">查看详情</el-button>
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>

    <pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" />
  </div>
</template>

<script>
import Pagination from '@/components/Pagination' // secondary package based on el-pagination

export default {
  name: 'Phone',
  components: { Pagination },
  data() {
    return {
      imageList: [],
      url: "https://img-blog.csdnimg.cn/20190826161431972.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3RyYW5zZm9ybWVyX1dTWg==,size_16,color_FFFFFF,t_70",
      currentDate: new Date(),
      total: 60,
      listQuery: {
        page: 1,
        limit: 12
      }
    }
  },
  created() {
    this.getList();
  },
  methods: {
    jumpToDetail(id) {
      this.$router.push({
          path: "/detail/index",
          query: {
              phoneId: id
          }
      });
    },
    getList() {
      this.imageList = [];
      for (let i = 0; i < this.listQuery.limit; i++) {
        let url = "";
        let brand = "";
        if (this.listQuery.page % 2 == 0) {
          url = "https://img-blog.csdnimg.cn/20190826161431972.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3RyYW5zZm9ybWVyX1dTWg==,size_16,color_FFFFFF,t_70";
          brand = "OPPO" + i;
        }
        else {
          url = "https://img-blog.csdnimg.cn/20190826162517464.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3RyYW5zZm9ybWVyX1dTWg==,size_16,color_FFFFFF,t_70";
          brand = "SAMSUNG" + i;
        }
        this.imageList.push({
          phoneId: (this.listQuery.page-1)*this.listQuery.limit + i,
          url: url,
          brand: brand
        })
      }
      console.log("page : " + this.listQuery.page);
      console.log("limit : " + this.listQuery.limit);
    }
  }
}
</script>

<style>
  .time {
    font-size: 13px;
    color: #999;
  }
  
  .bottom {
    margin-top: 13px;
    line-height: 12px;
  }

  .button {
    padding: 0;
    float: right;
  }

  .image {
    width: 100%;
    display: block;
  }

  .clearfix:before,
  .clearfix:after {
      display: table;
      content: "";
  }
  
  .clearfix:after {
      clear: both
  }
</style>
