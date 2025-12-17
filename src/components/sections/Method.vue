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
          How It Works: The SAGE Framework
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
              At <VueLatex expression="t=0" />, we leverage Vision Foundation Models (VFMs) like VGGT and SAM to estimate initial kinematic (<VueLatex expression="P_k^0" />) and structural (<VueLatex expression="P_s" />) **Analytic Concepts**.
            </p>
            <ul class="list-disc list-inside text-gray-600 space-y-2 pl-3">
              <li><strong>Structural Blueprints:</strong> Define the object's inherent spatial structure (e.g., hinge axis or rotational center).</li>
              <li><strong>Manipulation Blueprints:</strong> Define task-specific affordances and interaction routines.</li>
            </ul>
          </div>

          <div class="method-card">
            <h3 class="text-2xl font-bold mb-3 text-indigo-700">2. Dynamic Parameter Tracking (t > 0)</h3>
            <p class="text-gray-700 mb-4 border-l-4 border-indigo-300 pl-3">
              During interaction (<VueLatex expression="t > 0" />), the **Concept Expert** actively tracks the object's kinematic state (<VueLatex expression="P_k^t" />) using a Feature Alignment mechanism.
            </p>
            <div class="bg-indigo-100 p-4 rounded-lg text-sm font-mono text-indigo-900 overflow-x-auto shadow-inner">
              <span class="font-semibold text-gray-800">Feature Alignment Loss:</span>
              <VueLatex expression="\mathcal{L}_{align} = \mathbb{E}_{o_t}[1 - S_{cos}(Adapter(F_{VLA}), F_{Expert})]" display-mode />
            </div>
            <p class="text-xs text-gray-500 mt-2 pl-3">
                This mechanism bridges VLA internal features (<VueLatex expression="F_{VLA}" />) with the high-level Concept Expert features (<VueLatex expression="F_{Expert}" />).
            </p>
          </div>
        </div>
        
        <div class="method-card md:col-span-2">
            <h3 class="text-2xl font-bold mb-5 text-indigo-700">3. Explicit Knowledge Injection & Fine-Tuning</h3>
            <div class="grid md:grid-cols-2 gap-6">
                
                <div class="p-4 bg-white rounded-lg border border-gray-200 shadow-md">
                    <h4 class="font-bold text-xl mb-2 text-green-700">Kinematic Constraint Supervision (<VueLatex expression="\mathcal{L}_{kin}" />)</h4>
                    <p class="text-gray-700">
                        A supervised loss that forces the VLA's predicted action direction <VueLatex expression="v_{a_t}" /> to align with the physically valid constraint vector <VueLatex expression="v^*_t" /> derived directly from the Analytic Blueprints. This ensures spatial correctness.
                    </p>
                </div>

                <div class="p-4 bg-white rounded-lg border border-gray-200 shadow-md">
                    <h4 class="font-bold text-xl mb-2 text-green-700">Concept Derived Rewards (<VueLatex expression="\mathcal{R}_{AC}" />)</h4>
                    <p class="text-gray-700">
                        Provides dense, non-sparse rewards composed of kinematic progress and affordance alignment signals. This is used for Contrastive Learning (CQL) fine-tuning, drastically improving sample efficiency.
                    </p>
                </div>
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

/* Base Image Crop/Zoom CSS (Retained but simplified structure) */
.img-crop {
 border-radius: 16px;
  position: relative;
  display: block;
  width: 100%;
  aspect-ratio: 16 / 9; /* Define a wide aspect ratio for the overview */
  overflow: hidden; 
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
  background-color: #f3f4f6; 
}

/* Zoom Crop Strategy: Preserving the complex cropping logic provided by the user */
.img-crop .clipped-img {
  display: block;
  width: 180%; 
  max-width: none;
  
  /* Horizontal Crop (Centering) */
  margin-left: -34%;
  
  /* Vertical Crop */
  margin-top: -31%;    
  margin-bottom: -15%; 
  
  object-fit: cover;
}
</style>