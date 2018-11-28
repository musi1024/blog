# CSS常用数值单位 
一般在我们写CSS时用到最多数值单位，无非就是 px、em、rem、vh/vw，还有就是百分比（%）。

- px（像素）: 很容易理解，1px 就等屏幕的1像素，是个绝对单位，不会因为其他设置而变化。
- em : 1em 等于当前元素 font-size 的值，更准确来说，等于一个大写字母 M 或者一个汉字的宽度）
- rem : 跟 em 类似，但 1rem 是等于根元素 font-size 的值。
- vh/vw : 1vh/vw 分别等于是视口宽度的1%和视口高度的1%，很好用的单位，可是兼容性不太好。
- 百分比 : 也就是占父元素的百分比。

# 移动端适配方案
 1.  百分比
    优点 : 让所有元素都按站页面的百分比来计算，这样不管在PC端或者移动端，页面整体的比例都是一致的。
    缺点 : 宽度不确定，所以高度无法与宽度做任何配合
 2.  vh/vw 
    优点 : 可以根据屏幕的大小来设置，宽度和高度也能相配合
    缺点 : 兼容性不好
 3. 动态 rem
    优点 : 因为 1rem 等于根元素 font-size 的值，所有可以根据当前页面的大小来动态设置根元素的 font-size。
    缺点 ：那么每当用到 rem 就要计算元素的占比

# 更好地使用 rem
首先如何动态设置根元素的 font-size

    <script>
         var pageWidth = window.innerWidth
         document.write('<style>html{font-size:'+pageWidth/10 +'px;}</style>')
     </script>

把这段代码放在<header>底部去加载，那么你的根元素 font-size 就会动态地根据你页面的宽度来变化。那么这时 1rem 就等于当前页面的宽度的十分之一。
这里有需要注意的，一些浏览器例如Chrome，有默认的最小font-size，所以当你使用 rem 的时候需要注意，太小的元素就使用别的单位吧。
那么，现在问题来了，每次用到 rem 都要去算占多少比例，相当麻烦，所以应该使用到 sass。

    @function px( $px ){
        @return $px/$designWidth*10 + rem;
    } 
    $designWidth : 640; // 640是设计稿的宽度，你要根据设计稿的宽度填写.
    .child{
        width: px(320);
        height: px(160);
        margin: px(40) px(40);
        border: 1px solid red;
        float: left;
        font-size: 1.2em;
    }   
    

  
 
----------


那么以上是我学习移动端适配（rem方案）的记录。
 
