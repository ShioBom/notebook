#### vue-calender-component
##### 安装
```
npm i vue-calendar-component --save
cnpm i vue-calendar-component --save  //国内镜像
```
##### 使用
```
//vue文件中引入
import Calendar from 'vue-calendar-component';
 
 components: {
    Calendar
  }
    <Calendar
      v-on:choseDay="clickDay"
      v-on:changeMonth="changeDate"
      // v-on:isToday="clickToday"
      // :markDate=arr // arr=['2018/4/1','2018/4/3'] 标记4月1日和4月3日 简单标记
      //:markDateMore=arr // 多种不同的标记
      //第一个标记和第二个标记不能同时使用
      // :agoDayHide='1514937600' //某个日期以前的不允许点击  时间戳10位
      // :futureDayHide='1525104000' //某个日期以后的不允许点击  时间戳10位
      // :sundayStart="true" //默认是周一开始 当是true的时候 是周日开始
    ></Calendar>
 
    clickDay(data) {
      console.log(data); //选中某天
    },
    changeDate(data) {
      console.log(data); //左右点击切换月份
    },
    clickToday(data) {
      console.log(data); //跳到了本月
    }
 
  // 多个标记示例
  arr=[{date:'2018/4/1',className:"mark1"}, {date:'2018/4/13',className:"mark2"}];
  //4月1 标记的className是mark1 根据class做出一些标记样式
```