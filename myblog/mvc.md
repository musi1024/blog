## MVC 是什么
MVC 是一种设计模式（或者软件架构），把系统分为三层：Model数据、View视图和Controller控制器。

Model 数据管理，包括数据逻辑、数据请求、数据存储等功能。前端 Model 主要负责 AJAX 请求或者 LocalStorage 存储

View 负责用户界面，前端 View 主要负责 HTML 渲染。

Controller 负责处理 View 的事件，并更新 Model；也负责监听 Model 的变化，并更新 View，Controller 控制其他的所有流程。

MVC 三个部分各自负责自己的部分，并且单向联系，用户操作页面时， View 传送指令到 Controller，而 Controller 执行完处理后，通知 Model 改变状态，然后Model 将新的数据发送到 View，用户得到反馈。

代码示例：
~~~
{
  let view = {
    el: '#app',                           
    template: ``,
    render(data){                            
      let $el = $(this.el)
      $el.html(this.template)
    },
  }
  let model = {
    data: {},
    fetch: {},
    save: {}
  }
  let controller = {
    init(view, model){
      this.view = view
      this.model = model
      this.view.render(this.model.data)
    },
    bindEvent() {}
  }
   controller.init(view, model)
}
~~~

从上面代码里看出来，使用 MVC 编程逻辑会变得清晰，每一部分都有着自己的职责。但如果有多个页面或者模块的时候，难道每次都要重新写一次上面的类似代码吗？
所以我们应该使用面向对象，把重复的代码写到一个类。

代码如下：
~~~
class Model{
  constructor(options) {
    this.data = options.data
    this.id = options.id
  }
  fetch(id) {}
  create(data) {}
  destroy() {}
  update() {}
}

class View {
  constructor({el, template}) {
    this.el = el
    this.$el = $(el)
    this.template = template
  }
  render(data) {
    let html = this.template
    for (let key in data) {
      let value = data[key]
      html = html.replace(`__${key}__`, value)
    }
    this.$el.html(html)
  }
}

class Controller {
  constructor({view, model, events, init, ...rest }) {
    this.view = view 
    this.model = model
    Object.assign(this, rest)
    this.bindEvents()
    this.view.render(this.model.data)
    init.apply(this, arguments)
  }
  bindEvents() {
    this.events.map((e) => {
      this.view.$el.on(e.type, e.el, this[e.fn].bind(this))
    })
  }
}
~~~
如上面代码，把每一个模块的共有属性都在原型里，那么在下次需要用到 MVC 时，只需要用 new 就可以了,共有的属性都不用每次都写，只需要添加自由的属性即可。 

---

那么以上是我对 MVC 初步的学习和理解，之后还会继续加深学习。
