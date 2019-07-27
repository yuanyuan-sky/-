
![avatar](..\imgs\1055.png) 

	form表单只有get和post的提交方式，但是修改和删除对应的是PUT和DELETE  
	修改和删除还是使用POST，只是在相应的表单里埋一个hidden，name是_method，value是PUT和DELETE  
	这样spring就是进行PUT和DELETE解析

	
**form表单的enctype**  
![avatar](..\imgs\1066.png)