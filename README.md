# VUE-
VUE生命周期



<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="./vue.js"></script>
</head>
<body>
    <div id="app">
		<h3 id='h3'>{{msg}}</h3>
		
		<input type="button" value="修改msg" @click="msg='no'">
    </div>
</body>


<script>
    var vm= new Vue({
        el:"#app",
        data:{
			msg:'ok'
        },
        methods:{
            show(){
				console.log('执行了show方法（）')
			}
        },
		
		// 下面四个是实例创建期间的生命周期函数
		beforeCreate(){	//这是我们遇到的第一个生命周期函数,表示实例完全被创建出来之前,会执行它
			// console.log(this.msg);
			// this.show();
			// 注意:在beforeCreate生命周期函数执行的时候,data和methods中的数据都还没有被初始化
		},
		created(){	//这是我们遇到的第二个生命周期函数
			console.log(this.msg);
			this.show();
			//注意:在Created生命周期函数执行的时候,data和methods中的数据已经被初始化了
			// 如果要调用methods中方法和data中的数据,最早只能在created中进行操作
		},
		beforeMount() {	 	//这是我们遇到的第三个生命周期函数,表示模板已经在内存中编译完成了但是并未把模板渲染到页面中去
			console.log(document.getElementById("h3").innerText); 
		},
		mounted(){		//这是遇到的第四个生命周期函数,表示内存中的模板已经真实的挂载到了页面中,用户已经可以看到已经渲染好的页面了
			console.log(document.getElementById("h3").innerText); 
			// mounted是实例创建期间的最后一个生命周期函数,当执行完mounted就表示,实例已经被完全创建好了,此时如果没有其他操作的话,这个实例就会在内存中不再运动
		},
		
		
		// 接下来两个是运行中的两个生命周期函数
		beforeUpdate(){			//这个时候表示我们的界面还没有被更新	[数据是肯定被更新了的]
			console.log('界面上元素的内容：'+document.getElementById("h3").innerText); 
			console.log('data中的msg数据是：'+this.msg)
			// 结论:当执行beforeUpdate的时候,此时data的数据是最新的,但是页面还没有和最新的数据保持一致
		},
		updated() {
			console.log('界面上元素的内容：'+document.getElementById("h3").innerText); 
			console.log('data中的msg数据是：'+this.msg)
			// updated事件执行的时候页面和data数据已经保持同步了,都是最新的
		},
		
		
		// 当执行beforeDestory钩子函数的时候,vue实例就已经从运行阶段,进入到了销毁阶段,,实例身上所有的data和所有的methods以及过滤器都处于可用状态,
		// 此时还没有执行真正的销毁过程
		
		
		// 当执行到destory函数的时候,组件已经被完全销毁了,组件中的数据,方法,指令,过滤器都已经不可用了
	});
</script>
</html>
