#El

    el最早是jsti的。后来很好用就被jee引入到servlet-api.jar

${默认值.属性}  

###默认值：
1. pageScope/requestScope/sessionScope/applicationScope

        pageContext域/request域/session域/application域

        ${msg} 从最小的作用域开始找，直到找到为止


1. 获取参数列表

        ${param.ename}      相当于request.getParameter("ename");
        
        ${paramValues.like[0]}   //参数列表中的数组  
        paramValues相当于request.getParameterValues("");//获取参数列表中的数组

1. 对象属性

        ${对象.属性}    

#jstl:

1. 引入标签库

        <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"  %>
        前缀c
1. 语法
        

        1、<c: if test="${}">判定，test属性的值是boolean  

            not empty  不为空的意思
            <c:if test="${ not empty list}">
        
        2、<c:forEach items="${}" var=""  varStatus=""
            
            items：值是集合
            var :循环时集合中的每一个元素
            varStatus:是循环标量（存有信息）
                ①：index
                ②：count