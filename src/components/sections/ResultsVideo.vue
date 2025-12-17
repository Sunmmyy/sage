<script lang="ts" setup>
// 视频基础路径（不带尾部斜杠），例如：/video
const videoPath = '/video'

// 列表：文件名 + 显示标题 + 说明
const videos = [
    { file: 'storage.m4v', title: 'Place the stapler in the lower drawer.' },
    { file: 'kitchenpot.mp4', title: 'Place the cube in the kitchen pot.' },
    { file: 'microwave.mp4', title: 'Place the bowl in the microwave.' },
]
</script>

<template>
    <section id="results-videos" class="py-12">
        <el-row justify="center">
            <el-col :xs="24" :sm="24" :md="22" :lg="20" :xl="18">
                <el-card class="card">
                    <el-row justify="center">
                        <h3 class="text-2xl font-bold mb-4 text-gray-800 text-center">Real-World Manipulation Videos</h3>
                    </el-row>

                    <p class="text-gray-700 mb-6 text-center max-w-2xl mx-auto">
                        Below are selected real-world manipulation videos showcasing the SAGE framework's spatial guidance in action. 
                    </p>

                    <div class="video-grid">
                        <template v-for="v in videos" :key="v.file">
                            <div class="video-item">
                                <video
                                    class="video-player"
                                    controls
                                    preload="metadata"
                                    playsinline
                                    :src="`${videoPath}/${v.file}`"
                                >
                                    Your browser does not support the video tag.
                                </video>
                                <div class="video-meta">
                                    <div class="video-title">{{ v.title }}</div>
                                    <div class="video-desc">{{ v.desc }}</div>
                                </div>
                            </div>
                        </template>
                    </div>
                </el-card>
            </el-col>
        </el-row>
    </section>
</template>

<style scoped>
.card {
    margin-top: 20px;
    border-radius: 12px;
    overflow: hidden;
}

.video-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 18px;
    margin-top: 8px;
}

.video-item {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.video-player {
    width: 100%;
    aspect-ratio: 16/9;
    border-radius: 10px;
    background: #000;
    box-shadow: 0 8px 20px rgba(16,24,40,0.08);
    outline: none;
}

.video-meta {
    display: flex;
    flex-direction: column;
    gap: 4px;
}

.video-title {
    font-weight: 600;
    color: #0f172a;
}

.video-desc {
    color: #6b7280;
    font-size: 0.95rem;
}

/* Small responsive tuning */
@media (min-width: 1024px) {
    .video-grid { gap: 22px; }
}
</style>