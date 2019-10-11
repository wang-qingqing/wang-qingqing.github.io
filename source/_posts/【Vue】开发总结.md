---
title: 【Vue】开发总结
date: 2019-09-24
categories:  Vue
---
此篇文章用于记录vue开发过程中的总结。
<!--more-->
1. vue-router **动态路由匹配**
```
    /order/detail/:orderId

    在对应的components可以通过：this.$route.params.orderId 来获取路由上的 orderId。
```

2. v-html  **展示html解析后的内容**
```
    {{ }}：将元素当成纯文本输出
    v-text：会将元素当成纯文本输出
    v-html：会将元素当成HTML标签解析后输出

    <span v-html="item"></span>
```

3. 父组件传值给子组件 **props**
```
    父组件的引用：
    <child :info="info"></child>

    子组件内：
    props: {
        info: {
            type: Object,
            default() {
                return {}
            }
        }
    }
    props: {
        info: Object
    },
    或
    props: ['info']

```

4. 子组件调父组件的方法 **$emit**
```
    父组件有个方法：queryOrderList(requestParams)

    子组件想要调用父组件的这个方法：
    this.$emit('queryOrderList',requestParams);
```

5. template scope  **插槽**
```
    在使用el-table中，如果不能直接使用数据的字段，需要转换的时候，可以借助插槽来写。

    <el-table-column
        label="数量">
        <template slot-scope="scope">
            <span v-if="scope.row.adultCount > 0">{{scope.row.adultCount}}大</span>
        </template>
    </el-table-column>
```

6. filters **过滤器**
```
    filters: {     
        //日期格式化
        dateFormat (date,type){
            return dateUtils.dateFormat(date,type);
        },
    },

    <span>{{info.bookDate | dateFormat("YYYY-MM-DD")}}</span>

    filters的第一个参数就是|前面的字段，第二个参数是括号里的第一个，以此类推。

```

7. data
```
	data() {
    	return {
			info: {},
        }
    }
```

8. methods 方法
```
    methods: {
        a() {

        },
        b() {

        }
    }

    <button @click=”add(2,$event)”>add</button> 
    其中$event是包含了大部分鼠标事件的属性
```

9. created
```
    在生命周期created()的时候，可以发起异步接口请求。
```

10. components
```
    引入组件的方式：

    import orderTable from "xxx";
    components: {
	    orderTable
    }
```


11. 常用的plugin
```
    富文本编辑器：quill
    日期处理：moment
```

12. axios 接口调用的异常处理：**then...catch**
```
    建议使用catch这种捕获异常的处理方式：

    axios
        .post(url, requestParams)
        .then(resp => {
            if(resp.data && resp.data.success){
                //next handle
            }else{
                throw new Error(resp.data.msg);
            }   
        })
        .catch(err => this.$message({
            showClose: true,
            message: err,
            type: 'error'
        }));
```

13. v-model **用于表单数据的双向绑定**
```
    <el-input v-model="employeeName"></el-input>

    双向绑定数据                             
```

14. computed
```
    比较适合对多个变量或者对象进行处理后返回一个结果值
    
    computed: {
		orderStatusEnums() {
			return enums.orderStatus;
		},
    }
```

15. watch
```
    watch主要用于监控vue实例的变化，它监控的变量当然必须在data里面声明才可以，它可以监控一个变量，也可以是一个对象
```

16. v-for
```
    <div v-for="(item,key) in data" :key="item.id">
    </div>
```

17. 一个table，点击“添加”按钮，新增一行
```
    1. 先定义
    let addData = [];
    let addIndex = 0;

    2. 点击添加时，执行这个操作
    addData.push({
        index: addIndex++
    })

    3. 如果新增的每行都有个“删除”按钮，则传入当前行的index，执行以下操作
    for(let i = 0; i < addData.length;i++){
        if(index == addData[i].index){
            addData.splice(i,1);
        }
    }

    4. 在页面渲染addData时，需要设置key，防止出现显示问题。
    <addRow v-for="(item,key) in addData" :key="item.index">
    </addRow>
```

18. input、select等表单控件，校验不合法后，外边框标红
```
    1. 定义error的class
        .error {
            border: 1px solid #ff0000;
        }

    2. 定义error的标识字段
        data(){
            return {
                errorFlag: false,
                val: ''
            }
        }

    3. 绑定blur事件，用于触发合法性校验
        <input v-model="val"
            :class="errorClass"
            @blur="validate"></input>

        computed: {
            errorClass() {
                return this.errorFlag?"error":"";
            }
        }

    4. 合法性校验
        methods: {
            validate() {
                this.errorFlag = !this.val;
            }
        }
```

19. 





