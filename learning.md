## 写项目时需要注意的点：

1. 项目开发顺序，先画页面，再加功能，再加国际化

2. 项目中的CSS类名不要使用驼峰形式，而是采用class-name形式，组件引用next组件库里的，除非特殊情况，否则尽量不要修改组件的样式，应该尽量精简css,不要写无意义的样式

3. react组件中的函数不要用bind而是使用使用箭头函数声明例如：

onView = （）=> {
  this.setState({
      currentTab = xxx
  })
}

调用时用onClick = { this.onView }

4. 引用组件样式时，切换使用Tab，下拉选择使用Select， 搜索使用Search，表格使用Table，多个下拉选择和搜索组合
的若要放在水平方向上对其可以用Form inline

5. 修改样式组件的样式最好多看一下对应的API，使用API进行修改

6. 对于Tab组件，默认的显示值为defaultValue(误) ，当前的值为activeKey ,对于切换不同的Tab键就显示不同的内容的情况
可以把对应的组件放在tabItem中间，这样只要切换TAB就可以切换不同的内容了

7. 对于Select和Search组件要注意保存它们的筛选条件，保存在state中

8. Table组件中的title属性为列表的表头，indexkey用来对应请求到的数据中的字段，对于需要点击跳转详情页的表格需要
使用render函数，例如：

点击某一列单元格会跳转到详情页面，那么就需要在这列的TableColumn中绑定render函数，例如绑定一个operatorRender函数
cell={this.operatorRender}

operatorRender = (value,index,record) => {
  this.props.history.push('/myTask/detail/view/$(record.id).html')
}

record中就包含了点击的改行数据的所有字段，可以使用record.xxx来获取该字段，常用来获取对应数据的ID


9. 对于引号最好使用单引号''，避免使用双引号""


10. 对于翻页组件Pagination，pageNum代表当前点击要请求的第几页，pageSize代表每页显示的条数，total代表了
一共的条数，所以页数就自动会被计算出来为总条数除以每页的数据条数，需要注意的是翻译组件和table组件是共同使用的，
页数等于total除以固定的每页条数向上取整，最后一页的数据等于total模上pageSize

11. pagination居中显示的话可以直接设置style = {{textAlign:center}}

12. 向后台接口请求数据，目前本周学习到的是：一个组件若要想请求数据，需要设置三个文件，分别是container.js
,moudle.js 和 view.js 其中container的作用是将组件也就是view和module关联起来，要注意里面selector的值，就直接
设置为当前这个组件的state就好了，比如当前组件是sourceList那么就设置为sourceList.state 就可以了，
moudle负责设置具体的请求接口的函数，函数有两个参数，第一个是action，第二个参数是详细的请求数据的参数，

13. 请求数据时，一开始后端给的rap数据没有设置状态码code，所以一直在报错，后面设置以后就好了，以后要注意一下

14. view文件就是具体的组件，需要注意的一点是在componentDidMount中console.log(this.props)会发现里面没有请求到的data数据
而在module文件中却又可以console.log(data),可能是由于react自身的原因，组件在第一次挂载时，有些数据可能加载不全，所以打印值
最好是在render函数中去打印，因为render函数会多次渲染执行，而componentDidMount只是在页面第一次挂载时执行

15. example = (val) => {
  this.onView((val)=>{console.log(val)})
}

const val =1 

是无法打印出1的，因为onView 里面的箭头函数有一个形参，所以打印的时候里面的console.log(val)会打印出undefined，因为箭头函数并没有
传值进来，应该这样来写：
example = (val) => {
  this.onView(()=>{console.log(val)})
}

16. 在view组件中，写好样式后，要加各种功能函数，所有的切换tab,select 查询，翻页都是重新发起html请求，然后将请求到的数据重新渲染出来

会有一个函数是请求数据的函数，例如getData，或者loadData 第一个参数是action，第二个参数就是要配置的请求参数，其余各函数都是用来修改state中保存的状态

修改状态后，将state中状态拿到然后作为请求参数去请求数据

17. 组件中的筛选条件要保存好，最好放在URL中，这样就可以保证页面刷新而不会丢失筛选条件，具体待解决

18. 设计稿中的样式一定要高度还原，不能出现瑕疵，CSS还需要加强

19. 如何将页面撑满，待解决













