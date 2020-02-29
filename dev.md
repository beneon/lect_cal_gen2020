# 课程表数据挖掘与教学日历生成系统

## 2020-02-28

TODO: 教学日历中，对于校历调休应该加上自动时间跳转功能

这实际上是一个授课日期的跳转，从原先的安排往另外一个日期平移，但是需要注意的是，假期还是需要放的，所以假日那一天是相当于往None跳转

目前dates_adjustments的写法是：

```yaml
date_adjustments:
  - adjustment:
      from: 2020-04-06
      to: None
  - adjustment:
      from: 2020-05-04
      to: 2020-04-26
  - adjustment:
      from: 2020-05-05
      to: 2020-05-09
  - adjustment:
      from: 2020-06-25
      to: None
  - adjustment:
      from: 2020-06-26
      to: 2020-06-28
```


```python
[{'adjustment': {'from': datetime.date(2020, 4, 6), 'to': 'None'}},
 {'adjustment': {'from': datetime.date(2020, 5, 4),
   'to': datetime.date(2020, 4, 26)}},
 {'adjustment': {'from': datetime.date(2020, 5, 5),
   'to': datetime.date(2020, 5, 9)}},
 {'adjustment': {'from': datetime.date(2020, 6, 25), 'to': 'None'}},
 {'adjustment': {'from': datetime.date(2020, 6, 26),
   'to': datetime.date(2020, 6, 28)}}]
```

对于符合iso形式的文本会自动转换为日期，对于不符合的按照字符导入。

这个日期跳转的功能就做进conv.py的time_calulation里面吧，对于跳转到None的那些，我觉得应该选择输出错误信息。