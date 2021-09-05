---
title: 轮播图实现原理
tags: []
id: '123'
categories:
  - - 原生JS
date: 2018-09-13 15:44:57
---

轮播图可以说是最平常最基础不过的东西了，不论是web还是App方面，我本人也是拿来主义，是时候改变了，水平有限，总结出两种方案。 PS: 方案都很简陋，没有左右键切换，也没有下面表示进行的小圆点，只记录原理。 一.  通过display 控制 所谓轮播图就是将要展示的图片做好队列，但是窗口有限，一次只能展示一个图片，那么如果说通过display 设置 当前要展示的图片为 “block”，其他不展示的图片为 “none”，应该就解决这个问题了。 HTML代码：

    <div class="main" id="main">
        <div class="banner" id="banner">
            <img src="./images/1.png" alt="" class="banner-slide">
            <img src="./images/2.png" alt="" class="banner-slide">
            <img src="./images/3.png" alt="" class="banner-slide">
            <img src="./images/4.png" alt="" class="banner-slide">
        </div>
    </div>

  CSS代码：  

        .main {
            width: 1200px;
            height: auto;
            margin: 50px auto;
        }

        .banner {
            width: 600px;
            height: 460px;
            overflow: hidden;
        }

        .banner-slide {
            width: 600px;
            height: 460px;
        }

  JS代码：

        window.onload = function () {
            // 设置定时器
            var timer = null;
            // 设置 要优先显示 图片位置
            var index = 0;
            // 存储在内存中
            var pics = document.getElementsByClassName("banner-slide");

            function slideImg() {
                var main = document.getElementById("main");
                var banner = document.getElementById("banner");
                // 根据鼠标事件来 设置显示与否
                main.onmouseover = function () {
                    stopAutoPlay();
                }
                main.onmouseout = function () {
                    startAutoPlay();
                }
                main.onmouseout();
            }
            //开始播放轮播图
            function startAutoPlay() {
                timer = setInterval(function () {
                    index++;
                    if (index > 3) {
                        index = 0;
                    }
                    changeImg();
                }, 2000);
            }
            //暂停播放
            function stopAutoPlay() {
                if (timer) {
                    clearInterval(timer);
                }
            }
            //改变轮播图
            function changeImg() {
                for (var i = 0; i < pics.length; i++) {
                    pics\[i\].style.display = "none";
                }
                pics\[index\].style.display = "block";
            }
            slideImg();

        }