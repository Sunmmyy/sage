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
    model: 'SpatialVLA(FT)*', 
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
    row_class: 'highlight-mid' 
  },
  {
    model: '+SAGE-SFT',
    va_pick: 88.0, va_move: 70.8, va_drawer: 33.3,
    vm_pick: 76.4, vm_move: 73.6, vm_drawer: 55.6,
    avg: 66.3,
    row_class: 'highlight-sage'
  },
  { 
    model: 'OpenVLA-OFT', 
    va_pick: 65.3, va_move: 59.0, va_drawer: 12.2, 
    vm_pick: 72.3, vm_move: 69.6, vm_drawer: 47.2, 
    avg: 54.3, 
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
    pi_baseline: '60%', 
    pi_sage: '85%', 
  },
  { 
    task: 'Place the cube in the kitchen pot', 
    pi_baseline: '75%', 
    pi_sage: '90%', 
  },
  { 
    task: 'Place the bowl in the microwave', 
    pi_baseline: '50%', 
    pi_sage: '80%', 
  },
  {
    task: 'Place the green cube on the plate',
    pi_baseline: '90%',
    pi_sage: '100%',
  },
  {
    task: 'Stack blue bowl on middle then stack the pink bowl',
    pi_baseline: '60%',
    pi_sage: '90%',
  },
]

const tableDataAblation = [
  { setting: 'sage', ppo: '0.91', grpo: '0.79' },
  { setting: 'without_alignment', ppo: '0.86', grpo: '0.75' },
  { setting: 'kinematic_gt', ppo: '0.94', grpo: '0.82' },
  { setting: 'kinematic_structural_gt', ppo: '0.93', grpo: '0.84' },
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
            We evaluate SAGE in offline learning, online reinforcement learning, and real-world manipulation. Across these settings, explicit concept guidance improves both success rate and learning efficiency.
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
              <p class="result-note">
                On OpenVLA-OFT, SAGE-SFT raises average success from 54.3% to 69.0%, while SAGE-CQL reaches 71.7%. The gain is especially pronounced on the kinematically demanding Open/Close Drawer task. “FT” denotes fine-tuning; * marks a method designed specifically for 3D inputs.
              </p>

              <!-- <p class="text-sm text-gray-500 mt-4">
                The results are based on the Google Robot setup. **FT** denotes fine-tuned models. 
                <span class="font-bold text-blue-700">SAGE-CQL</span> achieves the highest average performance, demonstrating the effectiveness of dense rewards brought by Analytic Concepts (<VueLatex expression="\mathcal{R}_{AC}" />).
              </p> -->
            </el-tab-pane>

            <el-tab-pane label="Reinforcement Learning" name="RL">
              <h3 class="text-xl font-semibold mb-6 text-blue-600">Online Reinforcement Learning Results</h3>
              <p class="result-note mb-5">
                On the Open Drawer task, SAGE-enhanced PPO and GRPO converge faster and achieve higher final success rates. Across six ShapeNet-Mobility tasks—Faucet, Microwave, Laptop, StorageFurniture, KitchenPot, and Bucket—both SAGE variants consistently outperform their original baselines.
              </p>
              <el-row gutter="20" class="mb-4">
                <el-col :xs="24" :sm="24" :md="12">
                  <div class="text-center rl-image-container p-4 border rounded-lg shadow-sm bg-white">
                    <h4 class="font-bold text-lg mb-3 text-gray-800 border-b pb-2">Training Curve on Open Drawer Task. </h4>
                    <a href="./images/exp1.png" target="_blank" rel="noreferrer" class="block hover:opacity-90 transition">
                      <el-image src="./images/exp1.png" fit="cover" class="rounded-md border image-zoom-effect" />
                    </a>
                    
                  </div>
                </el-col>

                <el-col :xs="24" :sm="24" :md="12">
                  <div class="text-center rl-image-container p-4 border rounded-lg shadow-sm bg-white">
                    <h4 class="font-bold text-lg mb-3 text-gray-800 border-b pb-2">Final Success Rates on Six Challenging Manipulation Tasks</h4>
                    <a href="./images/exp2.png" target="_blank" rel="noreferrer" class="block hover:opacity-90 transition">
                      <el-image src="./images/exp2.png" fit="cover" class="rounded-md border image-zoom-effect" />
                    </a>
                   
                  </div>
                </el-col>
              </el-row>
              <h4 class="font-bold text-lg mb-3 text-gray-800">Ablation Study on Open Drawer</h4>
              <el-table :data="tableDataAblation" class="ablation-table">
                <el-table-column prop="setting" label="Setting" min-width="250">
                  <template #default="{ row }">
                    <span v-if="row.setting === 'sage'">SAGE</span>
                    <span v-else-if="row.setting === 'without_alignment'">
                      w/o <VueLatex expression="\mathcal{L}_{align}" />
                    </span>
                    <span v-else-if="row.setting === 'kinematic_gt'">
                      w. <VueLatex expression="P_k^{t*}" />
                    </span>
                    <span v-else>
                      w. <VueLatex expression="P_k^{t*}+P_s^*" />
                    </span>
                  </template>
                </el-table-column>
                <el-table-column prop="ppo" label="PPO" align="center" />
                <el-table-column prop="grpo" label="GRPO" align="center" />
              </el-table>
              <p class="result-note">
                Removing feature alignment reduces performance. Ground-truth kinematic or structural parameters provide only marginal gains, indicating that SAGE’s estimated parameters are already sufficiently accurate for policy learning.
              </p>
            </el-tab-pane>

            <el-tab-pane label="Real-World Validation" name="Qualitative">
              <h3 class="text-xl font-semibold mb-6 text-blue-600">Real-World Evaluation Results (20 Trials per Task)</h3>
              <p class="result-note mb-5">
                We evaluate π₀.₅ and π₀.₅ + SAGE-SFT on an AGILE PiPER dual-arm robot with Orbbec DABAI cameras. SAGE improves success across all five manipulation tasks.
              </p>
              
              <div class="mb-10">
                  <!-- <h4 class="font-bold mb-3 text-lg">Real-World Evaluation Results (Success Rate out of 20)</h4> -->
                  <el-table 
                      :data="tableDataRealWorld"
                      :show-header="true"
                      class="real-world-table"
                      :row-class-name="() => 'highlight-realworld-row'"
                  >
                      <el-table-column prop="task" label="Task Description" min-width="250" />
                      <el-table-column prop="pi_baseline" label="π₀.₅" align="center" width="150" />
                      <el-table-column prop="pi_sage" label="π₀.₅ + SAGE" align="center" width="150">
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

.result-note {
  margin-top: 16px;
  color: #4b5563;
  line-height: 1.7;
}

.ablation-table {
  margin-top: 12px;
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
