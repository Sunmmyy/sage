<script lang="ts">
import { defineComponent } from 'vue'
import { VueLatex } from 'vatex'

export default defineComponent({
  components: { VueLatex }
})
</script>

<template>
  <section id="methodology" class="py-16 bg-gray-50">
    <el-row justify="center">
      <el-col :xs="24" :sm="20" :md="16" :lg="12" :xl="12">
        
        <h2 class="text-4xl font-extrabold mb-12 text-center text-gray-800">
          Methodology: The SAGE Framework
        </h2>

        <div class="mb-14">
            <div class="img-crop shadow-2xl rounded-xl border border-gray-200 overflow-hidden">
                <img 
                    src="/overview-1.png" 
                    alt="SAGE Architecture" 
                    class="clipped-img" 
                />
            </div>
            <!-- <p class="text-sm text-gray-500 text-center mt-4 italic font-medium">
                <br>
                Figure 3. SAGE Architecture Overview. </p> -->
        </div>
        
        <div class="grid md:grid-cols-2 gap-8 mb-8">
          
          <div class="method-card">
            <h3 class="text-2xl font-bold mb-3 text-indigo-700">1. Analytic Concept Initialization (t=0)</h3>
            <p class="text-gray-700 mb-4 border-l-4 border-indigo-300 pl-3">
              Given the initial image and task instruction, a VLM identifies the task-relevant object and SAM segments an object-centric observation. VGGT extracts 3D-aware features, while a VLM-driven Concept Constructor instantiates the corresponding Manipulation Blueprint.
            </p>
            <ul class="list-disc list-inside text-gray-600 space-y-2 pl-3">
              <li><strong>Structural parameters <VueLatex expression="P_s" />:</strong> time-invariant geometry and kinematic structure, such as a hinge axis or sliding track.</li>
              <li><strong>Initial kinematic state <VueLatex expression="P_k^0" />:</strong> the initial state of movable components, estimated by fitting the blueprint to the observed object.</li>
            </ul>
          </div>

          <div class="method-card">
            <h3 class="text-2xl font-bold mb-3 text-indigo-700">2. Dynamic Parameter Tracking (t > 0)</h3>
            <p class="text-gray-700 mb-4 border-l-4 border-indigo-300 pl-3">
              During interaction, an Adapter maps intermediate VLA features into the VGGT spatial feature space. A Dynamic Parameter Head continuously estimates <VueLatex expression="P_k^t" />, with object-centric cross-attention improving sensitivity to boundaries and kinematic changes.
            </p>
            <div class="bg-indigo-100 p-4 rounded-lg text-sm font-mono text-indigo-900 overflow-x-auto shadow-inner">
              <span class="font-semibold text-gray-800">Feature Alignment:</span>
              <VueLatex expression="\mathcal{L}_{align}=\mathbb{E}_{o^{vis}}\left[\mathcal{S}_{cos}(\mathrm{Adapter}(\mathbf{F}_{VLA}),\mathbf{F}_{VGGT})\right]" display-mode />
            </div>
            <p class="text-xs text-gray-500 mt-2 pl-3">
                This alignment encourages the VLA representation to encode the explicit geometry and physical dynamics needed for manipulation.
            </p>
          </div>
        </div>
        
        <div class="method-card md:col-span-2">
            <h3 class="text-2xl font-bold mb-5 text-indigo-700">3. Explicit Knowledge Injection and VLA Fine-Tuning</h3>
            <div class="grid md:grid-cols-2 gap-6">
                
                <div class="p-4 bg-white rounded-lg border border-gray-200 shadow-md">
                    <h4 class="font-bold text-xl mb-2 text-green-700">Kinematic Constraint Supervision (<VueLatex expression="\mathcal{L}_{kcs}" />)</h4>
                    <p class="text-gray-700">
                        The Concept Expert derives an optimal 3D interaction direction <VueLatex expression="\boldsymbol{v}^*" /> from the current Analytic Concept. A cosine-distance loss aligns the translational action direction with this physically valid reference.
                    </p>
                    <VueLatex expression="\mathcal{L}_{kcs}=\mathbb{E}\left[1-\frac{\boldsymbol{v}_{\boldsymbol{a}_t}\cdot\boldsymbol{v}_t^*}{\|\boldsymbol{v}_{\boldsymbol{a}_t}\|\,\|\boldsymbol{v}_t^*\|}\right]" display-mode />
                </div>

                <div class="p-4 bg-white rounded-lg border border-gray-200 shadow-md">
                    <h4 class="font-bold text-xl mb-2 text-green-700">Concept Derived Rewards (<VueLatex expression="\mathcal{R}_{AC}" />)</h4>
                    <p class="text-gray-700">
                        For RL fine-tuning, SAGE combines a kinematic progress reward with an affordance alignment reward. The former measures progress toward the target state; the latter measures the 6D pose distance between the end effector and concept-derived grasp poses.
                    </p>
                    <VueLatex expression="\mathcal{R}_{AC}=w_{prog}\phi_{prog}+w_{afford}\phi_{afford}" display-mode />
                </div>
            </div>
            <div class="objective">
              <strong>Total objective:</strong>
              <VueLatex expression="\mathcal{L}_{total}=\mathcal{L}_{task}+\lambda_k\mathcal{L}_{kcs}+\lambda_a\mathcal{L}_{align}" display-mode />
            </div>
        </div>
      </el-col>
    </el-row>
  </section>
</template>

<style scoped>
/* Main Section Background and Padding */
#methodology {
    background-color: #ffffffff; /* light blue/gray background */
}

/* Card Style for Steps */
.method-card {
    background-color: #ffffff;
    padding: 30px;
    border-radius: 16px;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    transition: transform 0.3s ease;
}

.method-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 8px 10px -6px rgba(0, 0, 0, 0.1);
}

.objective {
  margin-top: 24px;
  padding: 18px;
  border-radius: 12px;
  background: #eef2ff;
  color: #312e81;
}

/* Base Image Crop/Zoom CSS (Retained but simplified structure) */
.img-crop {
  border-radius: 16px;
  position: relative;
  display: block;
  width: 100%;
  aspect-ratio: 16 / 9;
  overflow: hidden;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
  background-color: #f3f4f6; 
}

.img-crop .clipped-img {
  display: block;
  width: 138%;
  max-width: none;
  height: 138%;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  object-fit: contain;
}
</style>
