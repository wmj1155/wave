# 如何用canvas画出模仿360加速球中的波浪滚动
### 准备材料
1.一张静态图片，如下图

![alt text](/wave.png "波浪图")

2.用canvas画出圆形区域

·var wave = document.getElementById('wave');
 var canvas = document.createElement('canvas')
 if (!canvas.getContext) return;
 ctx = canvas.getContext('2d');
 canvasWidth = wave.offsetWidth;
 canvasHeight = wave.offsetHeight;
 canvas.setAttribute('width', canvasWidth);
 canvas.setAttribute('height', canvasHeight);
 wave.appendChild(canvas);·
 
 3.给图片增加相应的动画
 
 ·function loop () {
	ctx.clearRect(0, 0, canvasWidth, canvasHeight);
	if (!needAnimate) return;
	if (waveY < waveY_max) waveY += 1.5;
	if (waveX < waveX_min) waveX = 0; else waveX -= 3;
	      
	            ctx.globalCompositeOperation = 'source-over';
	            ctx.beginPath();
	            ctx.arc(canvasWidth/2, canvasHeight/2, canvasHeight/2, 0, Math.PI*2, true);
	            ctx.closePath();
	            ctx.fill();

	            ctx.globalCompositeOperation = 'source-in';
	            ctx.drawImage(waveImage, waveX, canvasHeight - 0.5*waveY);
	            
	            requestAnimationFrame(loop);
	        }·
