# AjaxNoteBook

# Fetch的各種用法

## 從Api中獲取json，呈現在前端畫面

 1. 先從後端取得json檔，這邊用這個網站示範
    `https://random-data-api.com/api/stripe/random_stripe`

    這個會產生隨機的json格式文件
    
    ```json
     {"id":2109,"uid":"0cd9df35-d870-4428-8926-2cd7f57384ec","valid_card":"2223003122003222","token":"tok_visa","invalid_card":"4000000000009235","month":"11","year":"2025","ccv":"621","ccv_amex":"6021"}
    ```
 2. 網頁這樣寫
    ```jsp
    <%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
    <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
        <!DOCTYPE html>
        <html>

        <head>
            <meta charset="UTF-8">
            <title>fetch示範頁面</title>
            <c:set var="contextRoot" value="${pageContext.request.contextPath}"></c:set>
            <link href="${contextRoot}/css/bootstrap.min.css" rel="stylesheet">
            <link rel="stylesheet" href="//code.jquery.com/ui/1.13.1/themes/base/jquery-ui.css">
            <link rel="stylesheet" href="/resources/demos/style.css">
            <script src="https://code.jquery.com/jquery-3.6.0.js"></script>
            <script src="https://code.jquery.com/ui/1.13.1/jquery-ui.js"></script>

        </head>

        <body>

            <div id="test">

            </div>
            <script>
                $(function() {
                    fetch("https://random-data-api.com/api/stripe/random_stripe").then(function(response) {
                        return response.json();
                    }).then(function(myJson) {
                        $("#test").append(`ID為:` + myJson.id).append(`<br>月份為` + myJson.month)
                    })
                })
            </script>

        </body>

        </html>
    ```
3. 網頁上看起來會像這樣
   ![image](https://user-images.githubusercontent.com/98711945/168445274-f735c105-3add-4477-a0f3-020bc4d27b07.png)



   




