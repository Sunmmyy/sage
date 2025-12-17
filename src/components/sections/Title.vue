<script lang="ts" setup>
// icons removed per request

// logo地址，已根据要求置为""
const logo = ''

// 标题
const title = 'Explicit Spatial Guidance from Object-Centric Concept Analysis for Vision-Language-Action Model Fine-Tuning'

// 标题颜色
const title_color = '#1f2937' // 更深的颜色，突出标题

// 标题补充，没有则置为''即可
const title_supp = ''

// 标题补充颜色
const title_supp_color = '#3b82f6' // 蓝色调

// 按钮颜色 (现在主要由 Element Plus 的 Plain/Primary 控制)
const btn_color = '#444444'

// 作者清单（包含作者姓名、头像、主页、地址序号）
const authors = [
  {
    name: "Mingyang Sun",
    address_flag: "1,4",
    is_corresponding: false,
    // is_equal: true // 假设 Mingyang Sun 是共一
  },
  {
    name: "Qichen He",
    address_flag: "2,4",
    is_corresponding: false,
    // is_equal: true // 假设 Qichen He 是共一
  },
  {
    name: "Xiujian Liang",
    address_flag: "3,4",
    is_corresponding: false,
    is_equal: false
  },
  {
    name: "Donglin Wang",
    address_flag: "1",
    is_corresponding: false,
    is_equal: false
  },
  {
    name: "Cewu Lu",
    address_flag: "2,4",
    is_corresponding: false,
    is_equal: false
  },
  {
    name: "Jianhua Sun",
    address_flag: "2",
    is_corresponding: true, // 假设 Jianhua Sun 是通讯作者
    is_equal: false
  },
]

// 地址清单（包含地址名称、头像、主页、地址序号）
const addresses = [
  {
    address_flag: "1",
    name: "Westlake University",
  },
  {
    address_flag: "2",
    name: "Shanghai Jiao Tong University",
  },
  {
    address_flag: "3",
    name: "Fudan University",
  },
  {
    address_flag: "4",
    name: "Shanghai Innovation Institute",
  },
]

// 共一和通讯提示
// 调整逻辑，根据作者列表自动生成上标
const getSuperscript = (author) => {
    let sup = author.address_flag ? author.address_flag : '';
    if (author.is_equal) {
        sup += '#';
    }
    if (author.is_corresponding) {
        sup += '*';
    }
    return sup;
}

const con_and_corresponding_author = 
  "#: Equal Contribution. *: Corresponding Author."

// 提供引导资料链接
const buttons = [
  {
    disabled: false,
    name: "Paper",
    link: "#", // 占位链接
  },
  {
    disabled: false,
    name: "Code",
    link: "https://github.com/JunyaoHu/academic-project-page-template-vue",
  },
]

// 最新消息 (保留，但使用更现代的 ElTag 样式)
const news = "🔥 [2024-12-15] This template project is still under development."

</script>

<template>
  <div class="hero">
    <div class="hero-overlay"></div>
    <el-row justify="center">
      <el-col :xs="24" :sm="22" :md="20" :lg="16" :xl="14">
        <div class="hero-inner text-center">
          
          <div class="title-wrap">
            <h1 class="paper-title">
              <span v-if="title" :style="{color:title_color}"> {{ title }}</span>
            </h1>
            <p v-if="title_supp" class="title-supp" :style="{color:title_supp_color}">{{ title_supp }}</p>
          </div>

          <div class="authors-list">
            <template v-for="(author, idx) in authors" :key="author.name">
              <span class="author-name">
                {{ author.name }}
                <sup v-if="author.address_flag || author.is_equal || author.is_corresponding" class="name_sup">{{ getSuperscript(author) }}</sup>
              </span>
              <span v-if="idx < authors.length - 1" class="author-separator">,</span>
            </template>
          </div>

          <div class="addresses" v-if="addresses && addresses.length">
            <template v-for="addr in addresses" :key="addr.address_flag">
              <el-tag class="address-tag" size="small" type="info"> 
                <sup class="address_sup">{{ addr.address_flag }}</sup> {{ addr.name }}
              </el-tag>
            </template>
          </div>

          <!-- <p class="con-cor text-gray-500 font-medium">{{ con_and_corresponding_author }}</p>
           -->
          <!-- <el-divider class="divider-thin" />

          <div class="actions">
            <a v-for="button in buttons" :key="button.name" :href="button.link || '#'" target="_blank">
              <el-button size="large" :disabled="button.disabled" type="primary">
                <span class="btn-text">{{ button.name }}</span>
              </el-button>
            </a>
          </div> -->

          <!-- <div class="news-alert-wrap">
            <el-tag class="news-tag" size="small" type="warning" effect="dark">{{ news }}</el-tag>
          </div> -->

        </div>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
/* Hero Section Styles */
.hero {
  position: relative;
  padding: 48px 0 36px;
  background: linear-gradient(180deg, rgba(240,248,255,0.9), rgba(245,247,250,0.8));
}
.hero-inner {
  padding: 18px;
  border-radius: 12px;
}

/* Title Styles */
.paper-title {
  font-family: "MyFont", "Times New Roman", Times, serif; /* 使用更正式的字体族 */
  font-weight: 800; /* 加粗标题 */
  letter-spacing: 0.5px;
  font-size: 36px; /* 增大字号 */
  margin: 0 auto 10px;
  line-height: 1.2;
  max-width: 900px;
}
.title-supp { 
    margin: 0 0 16px; 
    font-size: 18px;
    font-weight: 500;
}

/* Author Styles */
.authors-list {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 12px;
  font-size: 18px;
  color: #374151; /* Darker text */
}
.author-name {
    font-weight: 500;
    margin: 0 4px;
}
.author-separator {
    margin-right: 4px;
    font-weight: 400;
}
.name_sup {
  color: #606266; 
  font-size: 0.7em;
  vertical-align: super;
  margin-left: 2px;
  font-weight: bold;
}

/* Affiliation/Address Styles */
.addresses { 
    margin-top: 10px; 
    display:flex; 
    justify-content: center;
    gap: 8px; 
    flex-wrap:wrap; 
}
.address-tag { 
    background: #f3f4f6; /* Light background */
    color:#4b5563; 
    border: 1px solid #d1d5db;
    font-size: 13px;
    padding: 0 8px;
    height: 28px;
    line-height: 26px;
}
.address_sup {
  color: #606266; 
  margin-right: 3px;
  font-weight: bold;
}

/* Legend/Notes */
.con-cor {
  font-family: Arial, sans-serif;
  font-size: 14px;
  margin: 18px 0 10px;
}

/* Actions/Buttons */
.actions {
  margin-top: 20px;
}
.actions a {
  text-decoration: none;
  margin: 0 8px;
}
.btn-text {
  font-size: 16px;
  font-weight: 600;
}
.el-button--large {
  padding: 12px 20px;
}

/* News Tag */
.news-alert-wrap {
    margin-top: 20px;
}
.news-tag {
    font-size: 13px;
    height: 28px;
    line-height: 26px;
}

/* Utility */
.text-center { text-align: center; }
.divider-thin {
    max-width: 300px;
    margin: 20px auto;
}

/* Remove all other unnecessary styles */
/* .logo, .logo-wrap, 
.title-button, .title-button:hover, 
.guidance-button, .el-avatar, 
a:hover, a:-webkit-any-link, a { display logic removed in template }
*/
</style>