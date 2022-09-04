<template>
    <div class="container" @mouseover="stopAutoPlay" @mouseout="startAutoPlay" id="app">
        <!-- 图片的盒子 -->
        <div class="img-box">
            <img :src="item.image" alt="" v-for="(item,index) in list" :key="index">
        </div>
        <!-- 按钮的盒子 -->
        <div class="bottom-box" :style="{'--b-color':list[0].bottom_color}">
            <div class="l-box">
                <div class="title">{{list[active_index].title}}</div>
                <ul class="dots">
                    <li :class="[index==active_index?'pacman':'dot',is_prev?'1':'']" v-for="(item,index) in list" :key="index" @click="changeBanner(index)">
                        <!-- 吃豆人 -->
                        <div v-if="index==active_index"></div>
                        <div v-if="index==active_index"></div>
                    </li>
                </ul>
            </div>
            <div class="r-box">
                <i class="fa fa-angle-left" @click="changeBanner(-1,true)"></i>
                <i class="fa fa-angle-right" @click="changeBanner(-1,false)"></i>
            </div>
        </div>
    </div>
</template>

<script>
import { defaultComponent } from "vue";
export default defaultComponent({
    name: "app",
    setup() {
        // 定时器
        let timer = null;
        // 当前轮播的下标
        let active_index = 0;
        // 是否点击上一张（控制吃豆人的朝向）
        let is_prev = false;
        // 轮播图的数据
        let list = [
            {
                title: "标题一",
                image: "/images/150/1.jpg",
                bottom_color: "#AB2E3E",
            },
            {
                title: "标题二",
                image: "/images/150/2.jpg",
                bottom_color: "#2c84cd",
            },
            {
                title: "标题三",
                image: "/images/150/3.jpg",
                bottom_color: "#49a4d8",
            },
            {
                title: "标题四",
                image: "/images/150/4.jpg",
                bottom_color: "#4e4e4e",
            },
            {
                title: "标题五",
                image: "/images/150/5.jpg",
                bottom_color: "#623E26",
            },
            {
                title: "标题六",
                image: "/images/150/6.jpg",
                bottom_color: "#93504D",
            },
            {
                title: "标题七",
                image: "/images/150/7.jpg",
                bottom_color: "#212121",
            },
            {
                title: "标题八",
                image: "/images/150/8.jpg",
                bottom_color: "#000000",
            },
            {
                title: "标题九",
                image: "/images/150/9.jpg",
                bottom_color: "#972924",
            },
        ];

        // 停止轮播的函数
        const stopAutoPlay = () => {
            // 清空定时器
            for (let i = 0; i <= this.timer; i++) {
                clearInterval(i);
            }
        };

        // 开使轮播的函数
        const startAutoPlay = () => {
            // 停止轮播
            stopAutoPlay();
            timer = setInterval(() => {
                // 序号加一
                active_index++;
                if (active_index > list.length - 1) {
                    active_index = 0;
                }
                is_prev = false;
                changeBanner(active_index);
            }, 3000);
        };

        // 切换banner 参数index为轮播图的下标（点击上一张，下一张按钮的时候，该值为-1,；点击指示器时，该值为对应的轮播下标）
        // is_prev 为是否是上一张，上一张为true，下一张为false
        const changeBanner = (index, is_prev) => {
            if (index >= 0) {
                // 点击指示器的时候
                // 默认是下一张，吃豆人朝右
                is_prev = false;
                if (index < active_index) {
                    // 点击时轮播的下标小于当前轮播下标。则为上一张，吃豆人向左
                    is_prev = true;
                }
                // 设置当前的轮播下标
                active_index = index;
            } else {
                // 点击按钮时
                if (is_prev) {
                    // 上一张
                    this.active_index--;
                    if (active_index < 0) {
                        active_index = list.length - 1;
                    }
                } else {
                    // 下一张
                    active_index++;
                    if (active_index > list.length - 1) {
                        active_index = 0;
                    }
                }

                // 指明上一张或者下一张
            }

            // -mleft,-color是css的自定义属性，可以通过var函数进行调用
            // 设置偏移量以达到显示指定图片的目的
            document
                .querySelector(".img-box")
                .style.setProperty("--m-left", active_index);
            document
                .querySelector(".bottom-box")
                .style.setProperty(
                    "--b-color",
                    list[active_index].bottom_color
                );
        };

        return {
            timer,
            active_index,
            is_prev,
            list,
            stopAutoPlay,
            startAutoPlay,
            changeBanner,
        };
    },
});
</script>

<style>
* {
    margin: 0;
    padding: 0;
}
body {
    /* 100%窗口高度 */
    height: 100vh;
    /* 弹性布局 居中显示 */
    display: flex;
    justify-content: center;
    align-items: center;
    /* 渐变背景 */
    background: linear-gradient(200deg, #e6e9f0, #eef1f5);
}
li {
    list-style: none;
}
.container {
    width: 488px;
    height: 360px;
    border-radius: 6px;
    overflow: hidden;
}
.img-box {
    height: 275px;
    display: flex;
    /* 计算图片偏移量,--m-left是自定义属性,在js中赋值 */
    margin-left: calc(-488px * var(--m-left));
    /* 过渡 */
    transition: 0.35s;
}
.img-box img {
    width: 488px;
    height: 100%;
    object-fit: cover;
    object-position: center;
}
.bottom-box {
    /* 计算底部区域高度 */
    height: calc(360px - 275px);
    display: flex;
    /* --b-color是自定义属性，在js中会进行动态赋值 */
    --b-color: #000;
    background-color: var(--b-color);
    color: #fff;
    /* 相对定位 */
    position: relative;
}
/* 图片底部的渐变部分 */
.bottom-box::before {
    content: "";
    width: 100%;
    height: 50px;
    /* 背景渐变（透明——底部区域同色，上到下） */
    background: linear-gradient(to bottom, transparent, var(--b-color));
    /* 绝对定位 位置上移它的高度 */
    position: absolute;
    top: -50px;
}
/* 底部区域的左侧部分 */
.bottom-box .l-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding-left: 12px;
    /* 计算宽度 */
    width: calc(488px - 92px - 12px);
}
.bottom-box .title {
    width: 100%;
    font-size: 18px;
    line-height: 25px;
    /* 标题不换行，溢出显示省略号 */
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
.bottom-box .dots {
    display: flex;
    margin-top: 10px;
}
/* 指示器（小圆点） */
.bottom-box li {
    width: 8px;
    height: 8px;
    background-color: rgba(255, 255, 255, 0.4);
    margin: 4px;
    border-radius: 50%;
    cursor: pointer;
}
/* 指示器选中态（吃豆人） */
.bottom-box li.pacman {
    position: relative;
    width: 14px;
    height: 14px;
    background-color: transparent;
    margin-top: 1px;
}
/* 吃豆人由两个div组成 */
.bottom-box li.pacman div {
    width: 0;
    height: 0;
    border: 7px solid #fff;
    border-radius: 50%;
    border-right-width: 7px;
    border-right-color: transparent;
    /* 绝对定位 两个重合 */
    position: absolute;
}
/* 吃豆人朝向左 */
.bottom-box li.pacman.l {
    transform: rotate(180deg);
}
/* 接下来分别为吃豆人的两个部分设置动画 */
.bottom-box li.pacman div:nth-child(1) {
    /* 执行动画：动画名 时长 线性的 停留在最后一帧 */
    animation: pacman1 0.75s linear forwards;
}
.bottom-box li.pacman div:nth-child(2) {
    animation: pacman2 0.75s linear forwards;
}
/* 底部区域的右侧部分 */
.bottom-box .r-box {
    display: flex;
    padding-top: 12px;
    padding-left: 12px;
}
/* 上一页、下一页按钮 */
.bottom-box .r-box i {
    background-color: rgba(255, 255, 255, 0.1);
    width: 28px;
    height: 28px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 8px;
    font-size: 16px;
    margin-right: 12px;
}
.bottom-box .r-box i:hover {
    cursor: pointer;
    background-color: rgba(255, 255, 255, 0.2);
}

/* 定义吃豆人动画 */
@keyframes pacman1 {
    0% {
        transform: rotate(360deg);
    }
    40% {
        transform: rotate(270deg);
    }
    60% {
        transform: rotate(360deg);
    }
    100% {
        transform: rotate(270deg);
    }
}
@keyframes pacman2 {
    0% {
        transform: rotate(0deg);
    }
    40% {
        transform: rotate(90deg);
    }
    60% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(90deg);
    }
}
</style>