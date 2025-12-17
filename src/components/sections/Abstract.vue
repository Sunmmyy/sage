<!-- <script setup>
import abstract from '../mds/abstract.mdx';
</script>

<template>
  <div>
    <el-divider />

    <el-row justify="center">
        <el-col :xs="24" :sm="20" :md="16" :lg="12" :xl="12">
            <abstract />
        </el-col>
    </el-row>

  </div>
</template>

<style scoped> -->

<script setup>
import abstract from '../mds/abstract.mdx';
</script>

<template>
  <div class="abstract-section">
    <el-divider />

    <el-row justify="center">
      <el-col :xs="24" :sm="20" :md="16" :lg="12" :xl="12">
        <el-card class="abstract-card" shadow="hover">
          <div class="abstract-header">
            <h2>Abstract</h2>
            <p class="abstract-sub">A concise summary of the work</p>
          </div>

          <div class="abstract-body">
            <abstract />
          </div>
        </el-card>
      </el-col>
    </el-row>

  </div>
</template>

<style scoped>
.abstract-card {
  border-radius: 12px;
  padding: 1.25rem;
  background: linear-gradient(180deg, #ffffff 0%, #fbfbfd 100%);
  box-shadow: 0 6px 20px rgba(31, 45, 61, 0.06);
  transition: transform .16s ease, box-shadow .16s ease;
}
.abstract-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 30px rgba(31, 45, 61, 0.09);
}
.abstract-header {
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  gap: 0.75rem;
  margin-bottom: 0.75rem;
}
.abstract-header h2 {
  margin: 0;
  font-size: 1.4rem;
  letter-spacing: 1px;
  color: #222;
}
.abstract-sub {
  margin: 0;
  color: #7a7a86;
  font-size: 0.9rem;
}
.abstract-body {
  font-size: 1rem;
  line-height: 1.8rem;
  color: #333;
  text-align: justify;
}

/* make images inside the abstract responsive */
.abstract-body img {
  max-width: 100%;
  display: block;
  margin: 0.75rem auto;
  border-radius: 8px;
}

/* small screens: reduce padding */
@media (max-width: 576px) {
  .abstract-card {
    padding: 1rem;
  }
  .abstract-header h2 {
    font-size: 1.2rem;
  }
}
</style>