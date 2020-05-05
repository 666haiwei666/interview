# computed
 ## 定义
   是一个计算属性，类似于一个过滤器，对绑定到view的数据进行处理
 ## get和set用法
   ```````javaScript
   data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName：{
            get(){//回调函数 当需要读取当前属性值是执行，根据相关数据计算并返回当前属性的值
                return this.firstName + ' ' + this.lastName
            },
            set(val){//监视当前属性值的变化，当属性值发生变化时执行，更新相关的属性数据
                //val就是fullName的最新属性值
                console.log(val)
                    const names = val.split(' ');
                    console.log(names)
                    this.firstName = names[0];
                    this.lastName = names[1];
            }
     }
  }
   ```````
# watch
## 
 一个观察的动作
## 
 监听复杂数据类型需用深度监听,深度监听虽然可以监听到对象的变化,但是无法监听到具体对象里面那个属性的变化.oldVal和newVal值一样的原因是它们索引同一个对象/数组。Vue 不会保留修改之前值的副本
## 监听对象某个属性的变化
### 方法一  可以直接对用对象.属性的方法拿到属性
```````javaScript
   data(){
          return{
            'first':{
              second:0
            }
          }
        },
        watch:{
          first.second:function(newVal,oldVal){
            console.log(newVal,oldVal);
          }
    }
 
```````
### 方法二 watch如果想要监听对象的单个属性的变化,必须用computed作为中间件转化,因为computed可以取到对应的属性值

``````javaScript
    data(){
        return{
            'first':{
            second:0
            }
          }
        },
        computed:{
            secondChange(){
                return this.first.second
            }
        },
        watch:{
            secondChange(){
                console.log('second属性值变化了')
        }
    }
```````
# computed和watch的区别
1. 是计算值，
2. 应用：就是简化tempalte里面{{}}计算和处理props或$emit的传值
3. 具有缓存性，页面重新渲染值不变化,计算属性会立即返回之前的计算结果，而不必再次执行函数

3.2 watch特性
1. 是观察的动作，
2. 应用：监听props，$emit或本组件的值执行异步操作
3. 无缓存性，页面重新渲染时值不变化也会执行

