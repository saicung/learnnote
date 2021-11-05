### for 循环

**格式：**

	for 临时变量 in 序列:
	……

Ex：
	```python
	for i in range(0,10)  # range 左闭右开,只到10前一个数值9
	    print(i)
	```

**break：** 跳出整个循环。break之后的代码和剩余的循环将不会再执行，结束整个循环。
**continue：** 跳出当前循环。如果后面还有代码或者循环，将会继续执行。