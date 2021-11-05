### while 循环
	重复调用实现某一功能的代码块。

**格式：**

	while 表达式:
		……

Ex：
	```python
	num = 0
	while num < 10:
    	print(num)
    	num += 1
	```


**break：** 跳出整个循环。break之后的代码和剩余的循环将不会再执行，结束整个循环。
**continue：** 跳出当前循环。如果后面还有代码或者循环，将会继续执行。


### while 循环嵌套

	while 表达式:
		……
		while 表达式:
		……

Ex：
	```python
		i = 1
		num = 4
		while i <= num:
    		print(""*(num-1),end="")
    		x = 1
    		while x <= 2*i-1:
        		print("*",end="")
        		x += 1
    		print("")
    		i += 1
    ```