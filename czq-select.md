# czq-select(uniapp 小程序自定义select选项组件)

> #### `github 地址:` [**czq-selcet**](https://github.com/zhiqiang77/czq-select.git)   可以点个✨✨✨

---

> ## `使用方式:`

```ccc
...
<czq-select :cData="cData" v-model="value1" placeholder="请选择" class="ccc"></czq-select>

export default {
	data() {
		return {
			value1: 1,
			cData: [
				{
					id: 1,
					name: '九州'
				},
				{
					id: 2,
					name: '华夏'
				},
				{
					id: 3,
					name: '中华'
				},
				{
					id: 4,
					name: '神州'
				}
			]
		}
	}
}
...
```
------


## `属性:`
| 属性名 	| 类型  	 	 | 是否必填   | 默认值  	 |    说明               |
|:----------|:----------|:----------|:----------|:-----------------------|
| cData    	| Array	     |    	是   | ``` {id:0, name:'暂无数据'} ```|  选择时的数据  |
| multiple  |Boolean 或 String | 否    | false    | 是否多选      |
| placeholder    | String    | 否    | 请选择   | 数据为空时的提示文字        |
| v-model   |  Number   | 是   |    | 默认值 id       |
| cValue   | String 或 Number   | 否    |    | 默认值 name       |
| okText   | String   | 否   | 确定   | 确认按钮文字        | 
| cancelText| String    | 否    |  取消   |取消按钮文字        |



---
## `事件:`
| 事件名  | 说明  |
|:----------|:----------|
| onlySelect    | 返回当前选中的key或key和value的数组   |



##### tips：首次提交，多多指点。




......












