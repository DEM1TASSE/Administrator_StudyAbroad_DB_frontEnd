<template>
  <!-- <h1>这里是修改高校信息</h1> -->
  <el-container>
    <el-main>
      <el-card 
        class="box-card" 
        shadow="hover"
        style="height:auto"
      >
        <!-- <template #header> -->
          <div class="card-header">
            查询高校信息
          </div>
        <!-- </template> -->
        <el-row class="search">
          <el-col :span="8"></el-col>
          <el-col :span="5">
            <el-input v-model="search_word" placeholder="请输入高校名称" style="background:#e4e4e4">请输入高校名称</el-input>
          </el-col>
          <el-col :span="3">
            <el-button type="primary" round @click="getUniversityInfo()">查询高校</el-button>
          </el-col>
          <el-col :span="8"></el-col>
        </el-row>
        <div v-if="search_info==-1">
          <div class="call-word">搜索失败！高校不存在</div>
        </div>
        <div v-if="search_info==1" class="search-result">
          <div class="call-word">搜索成功！展示如下</div>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校id：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_id}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>
          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校名称：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_chname}}（{{this.university_enname}}）
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校校徽：
            </el-col>
            <el-col :span="10" style="text-align:left">
              <div>
                <el-avatar shape="circle" :src="this.university_badge"></el-avatar>
              </div>
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>
          
          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校简称：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_abbreviation}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校所在国家：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_country}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校所在地区：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_region}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校详细地址：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_location}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校邮箱：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_email}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校官网：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_website}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校学生人数：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_student_num}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校教师人数：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.university_teacher_num}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校院系：
            </el-col>
            <el-col :span="10" style="text-align:left">
              <div :v-for="college in university_college">
                {{college}}
              </div>
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校QS排名：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.QS_rank}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校THE排名：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.THE_rank}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

          <el-row>
            <el-col :span="5"></el-col>
            <el-col :span="6" style="text-align:left">
              高校USNEWS排名：
            </el-col>
            <el-col :span="10" style="text-align:left">
              {{this.USNEWS_rank}}
            </el-col>
            <el-col :span="3"></el-col>
          </el-row>

        </div>
      </el-card>
    </el-main>
  </el-container>
</template>

<script>
import axios from "axios";
import { ElMessage } from "element-plus";
export default {
  name: "ModifyUniversityInfo",
  data() {
    return {
      search_info: 0,
      search_word: "",

      university_id: "",
      university_chname: "",
      university_enname: "",
      university_badge: "",
      university_abbreviation: "",
      university_country: "",
      university_region: "",
      university_location: "",
      university_email: "",
      university_website: "",
      university_student_num: "",
      university_teacher_num: "",
      university_college: "",
      QS_rank: "",
      THE_rank: "",
      USNEWS_rank: "",
    };
  },
  methods: {
    getUniversityInfo() {
      console.log(this.search_word);
      axios.get("university/chname", {
        params: {
          chname: this.search_word,
        }
      })
      .then((res) => {
        console.log("搜索结果")
        console.log(res);
        if(!res.data.status) {
          this.search_info = -1;
        }
        else {
          this.search_info = 1;
          var source_data = res.data.data;
          console.log(source_data.university_id);
          axios.get("university/get_rank", {
            params: {
              university_id: res.data.data.university_id,
            }
          })
          .then((res) => {
            console.log(res);
            if(res.data.status) {
              this.QS_rank = res.data.data.rank[0].UniversityQsRank;
              this.THE_rank = res.data.data.rank[0].UniversityTheRank;
              this.USNEWS_rank = res.data.data.rank[0].UniversityUsnewsRank;
              this.university_id = source_data.university_id;
              this.university_chname = source_data.university_chname;
              this.university_enname = source_data.university_enname;
              this.university_badge = source_data.university_badge;
              this.university_abbreviation = source_data.university_abbreviation;
              this.university_country = source_data.university_country;
              this.university_region = source_data.university_region;
              this.university_location = source_data.university_location;
              this.university_email = source_data.university_email;
              this.university_website = source_data.university_website;
              this.university_student_num = source_data.university_student_num;
              this.university_teacher_num = source_data.university_teacher_num;
              this.university_college = source_data.university_college;
            }
          })
          .catch((err) => {
            console.log(err);
          })
        }
      })
      .catch((err) => {
        console.log(err);
        this.$alert('输入有误','警告', {
          confirmButtonText: '确定',
          callback: action => {
            this.search_word = "";
          }
        })
      });
    },
    updateUniversityInfo() {
      axios({
        url:"university"
      })
    }
  },
  components: {
    ElMessage,
  },
  created() {
    if (!this.$store.state.is_login) {
      ElMessage({
        message: "请先登录",
        type: "warning",
        showClose: true,
        duration: 2000,
      });
      /**之后此处需记录当前页面路径，以便于登陆完成后跳转 */
      this.$router.push({
        path: "/login",
        query: { redirect: this.$route.fullPath },
      });
    }

  },
};
</script>

<style scoped>
  .box-card {
    border-radius:10px;
    height:100%;
  }
  .card-header {
    font-family:SimSun;
    font-size:40px;
    font-weight:900;
    margin-left: 5%;
    margin-right: 70%;
    border-bottom: 6px grey solid;
  }
  .search {
    margin-top: 5%;
  }
  .call-word {
    border-bottom: 1px grey solid;
  }
  .el-row {
    margin-top: 1%;
    margin-bottom: 1%;
  }
</style>