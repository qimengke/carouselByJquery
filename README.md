# carouselByJquery
这是一个利用jquery语句实现轮播图的效果，代码少，易理解，设置了定时器，我的js代码为：
$(function (){
				// 获取轮播图中所有的图片
				var $imgs = $('#carousel img');
				// 定义一个公用的index，用于记录轮播到第几张了
				var index = 0;
				// 定义一个主轮播函数，进行轮播和index 的管理
				function carousel(){
					// 每次轮下一张
					index++;
					// 最后一张轮完回到第一张
					if(index == $imgs.size()){
						index = 0;
					}
					// 设置a标签的导航
					setNav(index);
					// 将第index张图片显示，同时其他图片隐藏
					$imgs.eq(index).fadeIn(500).siblings("img").fadeOut();
					
				}
				// 设置定时器，每2s轮播一次
				var timer = setInterval(carousel, 2000);
				
				// 定义一个函数用于设置轮播图的导航
				function setNav(ind){
					// 根据参数ind设置导航中第ind个a标签的背景为红色，而取消其他a标签的背景
					$('.nav a').eq(ind).addClass('active').siblings().removeClass();
				}
				
				// 给轮播导航添加点击事件
				$(".nav a").click(function (){
					// 停止轮播
					clearInterval(timer);
					// 获取点击的是第几个a标签, 将公共的index设置为这个几
					index = $(this).index();
					// 将对应的图片淡入，其他图片淡出
					$imgs.eq(index).fadeIn(500).siblings("img").fadeOut();
					// 同时将自己的背景设为红色，其他导航用a标签背景取消
					$(this).addClass('active').siblings().removeClass();
					// 继续从指定的图片开始轮播
					timer = setInterval(carousel, 2000);
				});
				
			});
			
