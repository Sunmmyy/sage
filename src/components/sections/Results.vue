<script lang="ts" setup>
import { VueLatex } from 'vatex'

// --- 1. SimplerEnv Benchmark (Table 1 Equivalent) ---
// SimplerEnv simulation evaluation results (Google Robot setup)
const tableDataSimplerEnv = [
  { 
    model: 'RT-1-X', 
    va_pick: 49.0, va_move: 32.3, va_drawer: 29.4, 
    vm_pick: 56.7, vm_move: 31.7, vm_drawer: 59.7, 
    avg: 43.1, 
    row_class: '' 
  },
  { 
    model: 'Octo-Base', 
    va_pick: 0.6, va_move: 3.1, va_drawer: 1.1, 
    vm_pick: 17.0, vm_move: 4.2, vm_drawer: 22.7, 
    avg: 8.1, 
    row_class: '' 
  },
  { 
    model: 'OpenVLA', 
    va_pick: 54.5, va_move: 47.7, va_drawer: 17.7, 
    vm_pick: 16.3, vm_move: 46.2, vm_drawer: 35.6, 
    avg: 36.3, 
    row_class: '' 
  },
  { 
    model: 'RoboVLM', 
    va_pick: 68.3, va_move: 56.0, va_drawer: 8.5, 
    vm_pick: 72.7, vm_move: 66.3, vm_drawer: 26.8, 
    avg: 49.8, 
    row_class: '' 
  },
  { 
    model: 'RoboVLM(FT)', 
    va_pick: 75.6, va_move: 60.0, va_drawer: 10.6, 
    vm_pick: 77.3, vm_move: 61.7, vm_drawer: 43.5, 
    avg: 54.8, 
    row_class: '' 
  },
  { 
    model: 'SpatialVLA', 
    va_pick: 89.5, va_move: 71.7, va_drawer: 68.8, 
    vm_pick: 81.0, vm_move: 69.6, vm_drawer: 59.3, 
    avg: 67.9, 
    row_class: '' 
  },
  { 
    model: 'SpatialVLA(FT)', 
    va_pick: 88.0, va_move: 72.7, va_drawer: 41.8, 
    vm_pick: 86.0, vm_move: 77.9, vm_drawer: 57.4, 
    avg: 70.6, 
    row_class: '' 
  },
  { 
    model: 'π₀', 
    va_pick: 75.2, va_move: 63.7, va_drawer: 25.6, 
    vm_pick: 72.7, vm_move: 65.3, vm_drawer: 38.3, 
    avg: 56.8, 
    row_class: '' 
  },
  // --- Mid-rule separation ---
  { 
    model: 'OpenVLA-OFT(FT)', 
    va_pick: 65.3, va_move: 59.0, va_drawer: 12.2, 
    vm_pick: 72.3, vm_move: 69.6, vm_drawer: 47.2, 
    avg: 66.0, 
    row_class: 'highlight-mid' 
  }, 
  { 
    model: '+SAGE-SFT', 
    va_pick: 83.3, va_move: 70.8, va_drawer: 41.7, 
    vm_pick: 80.6, vm_move: 75.0, vm_drawer: 62.5, 
    avg: 69.0, 
    row_class: 'highlight-sage' 
  },
  { 
    model: '+SAGE-CQL', 
    va_pick: 84.7, va_move: 73.6, va_drawer: 45.8, 
    vm_pick: 83.3, vm_move: 76.3, vm_drawer: 66.7, 
    avg: 71.7, 
    row_class: 'highlight-best' 
  },
]

// --- 2. Real-World Evaluation (New Table) ---
const tableDataRealWorld = [
  { 
    task: 'Place the stapler in the lower drawer', 
    pi_baseline: '12/20', 
    pi_sage: '17/20', 
  },
  { 
    task: 'Place the cube in the kitchen pot', 
    pi_baseline: '15/20', 
    pi_sage: '18/20', 
  },
  { 
    task: 'Place the bowl in the microwave', 
    pi_baseline: '10/20', 
    pi_sage: '16/20', 
  },
]

// --- 3. Reinforcement Learning Summary ---
const tableDataRL = [
  {
    experiment: 'CQL Fine-tune',
    reward: 'Analytic Concept Reward',
    avg_return: 123.4,
    success: '72/100'
  },
  {
    experiment: 'Behavioral Cloning',
    reward: 'Imitation',
    avg_return: 98.1,
    success: '58/100'
  },
  {
    experiment: 'PPO Baseline',
    reward: 'Shaped Reward',
    avg_return: 110.7,
    success: '65/100'
  },
]


/**
 * Sets the row style based on a custom class name in the data row
 */
const tableRowClassName = ({ row }) => {
  // Use custom classes only for the SimplerEnv table for specific highlights
  if (row.row_class) {
      return row.row_class;
  }
  return '';
}
</script>

<template>
  <section id="results" class="py-12">
    <el-divider />

    <el-row justify="center">
      <h2 class="text-3xl font-bold mb-8 text-center section-title">Experimental Results</h2>
    </el-row>

    <el-row justify="center">
      <el-col :xs="24" :sm="24" :md="22" :lg="20" :xl="18">
        <el-card class="card">
          <p class="mb-4 text-gray-700">
            We evaluated the SAGE framework, focusing on its performance gain on **SimplerEnv** tasks and its superior **Qualitative Results** in complex manipulation.
          </p>

          <el-tabs class="demo-tabs" model-value="SimplerEnv">

            <el-tab-pane label="SimplerEnv Benchmark" name="SimplerEnv">
              <h3 class="text-xl font-semibold mb-4 text-blue-600">SimplerEnv Manipulation Task Performance (Success Rate %)</h3>
              
              <div class="table-container">
                <el-table 
                  :data="tableDataSimplerEnv"
                  :row-class-name="tableRowClassName"
                  max-height="500"
                >
                  <el-table-column prop="model" label="Model" width="160" fixed sortable/>
                  
                  <el-table-column label="Variant Aggregation" align="center">
                      <el-table-column prop="va_pick" label="Pick Coke Can" min-width="120" sortable>
                        <template #default="{ row }">
                            {{ row.va_pick.toFixed(1) }}%
                        </template>
                      </el-table-column>
                      <el-table-column prop="va_move" label="Move Near" min-width="120" sortable>
                        <template #default="{ row }">
                            {{ row.va_move.toFixed(1) }}%
                        </template>
                      </el-table-column>
                      <el-table-column prop="va_drawer" label="Open/Close Drawer" min-width="120" sortable>
                        <template #default="{ row }">
                            {{ row.va_drawer.toFixed(1) }}%
                        </template>
                      </el-table-column>
                  </el-table-column>

                  <el-table-column label="Visual Matching" align="center">
                      <el-table-column prop="vm_pick" label="Pick Coke Can" min-width="120" sortable>
                        <template #default="{ row }">
                            {{ row.vm_pick.toFixed(1) }}%
                        </template>
                      </el-table-column>
                      <el-table-column prop="vm_move" label="Move Near" min-width="120" sortable>
                        <template #default="{ row }">
                            {{ row.vm_move.toFixed(1) }}%
                        </template>
                      </el-table-column>
                      <el-table-column prop="vm_drawer" label="Open/Close Drawer" min-width="120" sortable>
                        <template #default="{ row }">
                            {{ row.vm_drawer.toFixed(1) }}%
                        </template>
                      </el-table-column>
                  </el-table-column>
                  
                  <el-table-column prop="avg" label="Avg" width="80" sortable>
                    <template #default="{ row }">
                        <span :class="{'font-bold text-blue-700': row.avg === 71.7}">
                            {{ row.avg.toFixed(1) }}%
                        </span>
                    </template>
                  </el-table-column>
                </el-table>
              </div>

              <!-- <p class="text-sm text-gray-500 mt-4">
                The results are based on the Google Robot setup. **FT** denotes fine-tuned models. 
                <span class="font-bold text-blue-700">SAGE-CQL</span> achieves the highest average performance, demonstrating the effectiveness of dense rewards brought by Analytic Concepts (<VueLatex expression="\mathcal{R}_{AC}" />).
              </p> -->
            </el-tab-pane>

<el-tab-pane label="Reinforcement Learning" name="RL">
              <h3 class="text-xl font-semibold mb-6 text-blue-600">Online Reinforcement Learning Results</h3>
              <el-row gutter="20" class="mb-4">
                <el-col :xs="24" :sm="24" :md="12">
                  <div class="text-center rl-image-container p-4 border rounded-lg shadow-sm bg-white">
                    <h4 class="font-bold text-lg mb-3 text-gray-800 border-b pb-2">Training Curve on Open Drawer Task. </h4>
                    <a href="/images/exp1.png" target="_blank" rel="noreferrer" class="block hover:opacity-90 transition">
                      <el-image src="/images/exp1.png" fit="cover" class="rounded-md border image-zoom-effect" />
                    </a>
                    
                  </div>
                </el-col>

                <el-col :xs="24" :sm="24" :md="12">
                  <div class="text-center rl-image-container p-4 border rounded-lg shadow-sm bg-white">
                    <h4 class="font-bold text-lg mb-3 text-gray-800 border-b pb-2">Final Success Rates on Six Challenging Manipulation Tasks</h4>
                    <a href="/images/exp2.png" target="_blank" rel="noreferrer" class="block hover:opacity-90 transition">
                      <el-image src="/images/exp2.png" fit="cover" class="rounded-md border image-zoom-effect" />
                    </a>
                   
                  </div>
                </el-col>
              </el-row>
            
            </el-tab-pane>

            <el-tab-pane label="Real-World Validation" name="Qualitative">
              <h3 class="text-xl font-semibold mb-6 text-blue-600">Real-World Evaluation Results (Success Rate out of 20)</h3>
              
              <div class="mb-10">
                  <!-- <h4 class="font-bold mb-3 text-lg">Real-World Evaluation Results (Success Rate out of 20)</h4> -->
                  <el-table 
                      :data="tableDataRealWorld"
                      :show-header="true"
                      class="real-world-table"
                      :row-class-name="() => 'highlight-realworld-row'"
                  >
                      <el-table-column prop="task" label="Task Description" min-width="250" />
                      <el-table-column prop="pi_baseline" label="Baseline ($\pi_{0.5}$)" align="center" width="150" />
                      <el-table-column prop="pi_sage" label="SAGE ($\pi_{0.5}$+SAGE)" align="center" width="150">
                          <template #default="{ row }">
                              <span class="font-bold text-green-700">
                                  {{ row.pi_sage }}
                              </span>
                          </template>
                      </el-table-column>
                  </el-table>
                  <!-- <p class="text-sm text-gray-500 mt-2">
                      Real-world evaluation results showing SAGE's improved success rates over the baseline model ($\pi_{0.5}$).
                  </p> -->
              </div>
            </el-tab-pane>


          </el-tabs>
        </el-card>
      </el-col>
    </el-row>
  </section>
</template>

<style scoped>
.section-title {
  color: #1f2937; /* Dark text for section title */
}
.card {
  margin-top: 20px;
  border-radius: 12px;
  overflow: hidden; /* Ensure card content respects border-radius */
}

/* Custom row classes for highlighting SimplerEnv results */
.highlight-best {
  background-color: #e0f2fe; /* light-blue-100 */
  font-weight: 600; /* Semi-bold */
}

.highlight-sage {
  background-color: #f0f9ff; /* light-blue-50 */
}

.highlight-mid {
  background-color: #f3f4f6; /* gray-100 */
  border-top: 2px solid #9ca3af; /* A visible line */
}

/* Custom row style for the Real-World table */
.highlight-realworld-row {
  background-color: #f7fee7; /* light-lime-50, for a subtle difference */
}


/* Element Plus table header style refinement */
:deep(.el-table .el-table__header-wrapper th) {
  background-color: #e5e7eb !important; /* light gray for header background */
  color: #1f2937;
  font-weight: 700;
  border-bottom: 1px solid #d1d5db;
}

/* Ensure nested header columns have a clean look */
:deep(.el-table th.is-group) {
    background-color: #f3f4f6 !important; /* Slightly lighter gray for the group header */
}

/* Reinforcement Learning images grid */
.rl-images-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 16px;
}

.rl-image {
  width: 100%;
  aspect-ratio: 16/9;
  border-radius: 10px;
  box-shadow: 0 8px 20px rgba(16,24,40,0.06);
  overflow: hidden;
}

.image-placeholder {
  display:flex; align-items:center; justify-content:center; height:100%; background:#f3f4f6; color:#6b7280; font-weight:600;
}

/* RL image card styles */
.rl-card {
  border-radius: 10px;
  overflow: hidden;
  background: #fff;
  box-shadow: 0 8px 20px rgba(16,24,40,0.06);
}

.rl-caption {
  padding: 10px 12px; color: #374151; font-weight: 600; text-align: left;
}

@media (max-width: 640px) {
  .rl-image { aspect-ratio: 16/9; }
}

/* Make anchor wrappers block-level so image + caption layout correctly */
.img-link, .rl-card > a {
  display: block;
  text-decoration: none;
}

/* RL Image styles */
.rl-image-container .rl-image {
    max-height: 350px; /* Limit height for uniform look */
    width: 100%;
}

/* Ensure el-image inner img covers when fit=cover */
.rl-image-container :deep(.el-image__inner) {
  object-fit: cover !important;
  width: 100% !important;
  height: 100% !important;
}

/* Ensure caption sits below the image */
.rl-card .rl-caption { margin-top: 8px; }
</style>