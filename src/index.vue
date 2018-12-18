<template>
    <div>
        <gcanvas v-if="isWeex" ref="canvas_holder" style="width:750px;height:400px;"></gcanvas>
        <canvas v-if="!isWeex" ref="canvas_holder" style="width:100%;height:100%;"></canvas>
    </div>
</template>
<script>
import F2Extend from './lib/F2.js';
import F2 from '@antv/f2';
const isWeex = weex.config.env.platform !== 'Web'
const { enable, WeexBridge, Image: GImage } = require('gcanvas.js');
const EnvImage = !isWeex ? Image : GImage;

export default {
    data() {
        return {
            isWeex: isWeex ? 1 : 0
        },

        // 绘制红色区域
        renderRedRect () {
            let ref = this.$refs.canvas_holder;
            if (isWeex) {
                ref = enable(ref, {bridge: WeexBridge});
            }
            var ctx = ref.getContext('2d');

            // 可以绘制出一个红色区域, 说明 Gcanvas 确实引入成功
            ctx.fillStyle = 'red';
            ctx.fillRect(0, 0, 100, 100);
        },

        // 直接使用 F2
        renderNativeF2 () {
            let ref = this.$refs.canvas_holder;
            if (isWeex) {
                ref = enable(ref, {bridge: WeexBridge});
            }
            var ctx = ref.getContext('2d');

            // F2 对数据源格式的要求，仅仅是 JSON 数组，数组的每个元素是一个标准 JSON 对象。
            const data = [
                { genre: 'Sports', sold: 275 },
                { genre: 'Strategy', sold: 115 },
                { genre: 'Action', sold: 120 },
                { genre: 'Shooter', sold: 350 },
                { genre: 'Other', sold: 150 },
            ];

            // Step 1: 创建 Chart 对象
            const chart = new F2.Chart({
                context: ctx,
                width: 750,
                height: 400
            });

            // Step 2: 载入数据源
            chart.source(data);

            // Step 3：创建图形语法，绘制柱状图，由 genre 和 sold 两个属性决定图形位置，genre 映射至 x 轴，sold 映射至 y 轴
            chart.interval().position('genre*sold').color('genre');

            // Step 4: 渲染图表
            chart.render();
        },

        renderF2Extend () {
            let ref = this.$refs.canvas_holder;
            if (isWeex) {
                ref = enable(ref, {bridge: WeexBridge});
            }
            var ctx = ref.getContext('2d');
            var canvas = new F2Extend.Renderer(ctx);

            // F2 对数据源格式的要求，仅仅是 JSON 数组，数组的每个元素是一个标准 JSON 对象。
            const data = [
                { genre: 'Sports', sold: 275 },
                { genre: 'Strategy', sold: 115 },
                { genre: 'Action', sold: 120 },
                { genre: 'Shooter', sold: 350 },
                { genre: 'Other', sold: 150 },
            ];

            // Step 1: 创建 Chart 对象
            const chart = new F2Extend.Chart({
                context: ctx,
                width: 750,
                height: 400
            });

            // Step 2: 载入数据源
            chart.source(data);

            // Step 3：创建图形语法，绘制柱状图，由 genre 和 sold 两个属性决定图形位置，genre 映射至 x 轴，sold 映射至 y 轴
            chart.interval().position('genre*sold').color('genre');

            // Step 4: 渲染图表
            chart.render();
        }
    },
    mounted: function () {
        // 绘制红色区域, 检测是否引入 Gcanvas
        this.renderRedRect();

        // 直接使用 F2 绘制图表
        // this.renderNativeF2();

        // 使用扩展的 F2 绘制图表
        // this.renderF2Extend();
    }
};
</script>
