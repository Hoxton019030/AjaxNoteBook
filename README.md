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
   

## 如果取得的json是個陣列的話

 以下使用這段json示範
 ```
 [{"id":16,"date":"2022-05-14T04:29:17.788+00:00","title":"標題","contentOfNews":"內容","imageOfNews":"data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAIBAQIBAQICAgICAgICAwUDAwMDAwYEBAMFBwYHBwcGBwcICQsJCAgKCAcHCg0KCgsMDAwMBwkODw0MDgsMDAz/2wBDAQICAgMDAwYDAwYMCAcIDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAz/wAARCABJAFwDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD+f+iiigAooooAKKKKACiiigAooooAKKKKACiiigAoor0T9ln9mnXf2ufjLa+B/Dd3pNlq13p+o6kkupSyR24jsbGe+lBaNHbcYrdwvy4LFQSoJYHRy6JNv0Su38kgPO6KKKACivRPA/7NOu+P/wBnDx98ULO70mPQPh1qGk6bqVvNLILyeTUTciAwqEKMq/ZZN+51I3LgNk487oeknF7q34pNfg0/mAUUUUAFFFFABRRRQAV9q/8ABAv4ueLPhr/wUFsrPwz4m8Q6BFr3hfxLHdwaZqM1quovFoOozWyyLGw8wpOsbxg52yKrLhgDXxVWr4H8da38MfF+neIPDesar4e1/R51urDUtMu5LS8sZlOVkiljIdHB6MpBFNP3ZR25oyjftzRcb/K9xP0v/wAA/Rj9mr45J4a/4JqeIfjJqPxp+OHgz4peK/iU+jeNvH3hDSF8R+J5LRbCCXT7S5vZ9VsZ7W3mdbl8pI4uHtlV+IUFbaft7fDyy/aV+J2o+HtO+Pnwht/jHaeGLZ/ir4X8PwaF4m0bWfsHmTO1jb3DLJY6rMUvpbeC9ikl2LIDLtUH4G8K/ttfGfwJ8Udc8caJ8XPido3jTxMgj1jxBY+Kb631TVlG0hbi5SUSyj5E4dj91fQVH8P/ANtD4xfCbxx4i8TeFvix8S/DXiTxfKZ9e1bSvE97Z32tyF2cvdTRyq87F3dsyFjliepNUprn5mtLR0Tta0YxaT3SfLzXXLZ2upW1nlag4p63er63k5Xa2utI630uk430++dS+JXxr/Y9/Y6/bm8A/wDC3vEp1nwJ8SfD9lNdeGNZuNOsQ11dasmoSQQQtGtulw4iE0aqoLKqODtAr8u67H4UftD+P/gNqOq3ngbxz4w8GXeu2rWOpT6FrNzp0mo27HLQzNC6mSMkAlWyCe1cdXPTpuLvJ3doLa3wwUNl092/k21bS73qzUpPl0V2183f7/8ALcKKKK1MwooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooA//2Q==","relevant_Currency1":"BTC","relevant_Currency2":null,"relevant_Currency5":null,"relevant_Currency4":null,"relevant_Currency10":null,"relevant_Currency9":null,"relevant_Currency3":null,"relevant_Currency6":null,"relevant_Currency8":null,"relevant_Currency7":null},{"id":15,"date":"2022-05-14T04:29:17.111+00:00","title":"標題","contentOfNews":"內容","imageOfNews":"data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAIBAQIBAQICAgICAgICAwUDAwMDAwYEBAMFBwYHBwcGBwcICQsJCAgKCAcHCg0KCgsMDAwMBwkODw0MDgsMDAz/2wBDAQICAgMDAwYDAwYMCAcIDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAz/wAARCABJAFwDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD+f+iiigAooooAKKKKACiiigAooooAKKKKACiiigAoor0T9ln9mnXf2ufjLa+B/Dd3pNlq13p+o6kkupSyR24jsbGe+lBaNHbcYrdwvy4LFQSoJYHRy6JNv0Su38kgPO6KKKACivRPA/7NOu+P/wBnDx98ULO70mPQPh1qGk6bqVvNLILyeTUTciAwqEKMq/ZZN+51I3LgNk487oeknF7q34pNfg0/mAUUUUAFFFFABRRRQAV9q/8ABAv4ueLPhr/wUFsrPwz4m8Q6BFr3hfxLHdwaZqM1quovFoOozWyyLGw8wpOsbxg52yKrLhgDXxVWr4H8da38MfF+neIPDesar4e1/R51urDUtMu5LS8sZlOVkiljIdHB6MpBFNP3ZR25oyjftzRcb/K9xP0v/wAA/Rj9mr45J4a/4JqeIfjJqPxp+OHgz4peK/iU+jeNvH3hDSF8R+J5LRbCCXT7S5vZ9VsZ7W3mdbl8pI4uHtlV+IUFbaft7fDyy/aV+J2o+HtO+Pnwht/jHaeGLZ/ir4X8PwaF4m0bWfsHmTO1jb3DLJY6rMUvpbeC9ikl2LIDLtUH4G8K/ttfGfwJ8Udc8caJ8XPido3jTxMgj1jxBY+Kb631TVlG0hbi5SUSyj5E4dj91fQVH8P/ANtD4xfCbxx4i8TeFvix8S/DXiTxfKZ9e1bSvE97Z32tyF2cvdTRyq87F3dsyFjliepNUprn5mtLR0Tta0YxaT3SfLzXXLZ2upW1nlag4p63er63k5Xa2utI630uk430++dS+JXxr/Y9/Y6/bm8A/wDC3vEp1nwJ8SfD9lNdeGNZuNOsQ11dasmoSQQQtGtulw4iE0aqoLKqODtAr8u67H4UftD+P/gNqOq3ngbxz4w8GXeu2rWOpT6FrNzp0mo27HLQzNC6mSMkAlWyCe1cdXPTpuLvJ3doLa3wwUNl092/k21bS73qzUpPl0V2183f7/8ALcKKKK1MwooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooA//2Q==","relevant_Currency1":"BTC","relevant_Currency2":null,"relevant_Currency5":null,"relevant_Currency4":null,"relevant_Currency10":null,"relevant_Currency9":null,"relevant_Currency3":null,"relevant_Currency6":null,"relevant_Currency8":null,"relevant_Currency7":null},{"id":14,"date":"2022-05-14T04:29:13.930+00:00","title":"標題","contentOfNews":"內容","imageOfNews":"data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAIBAQIBAQICAgICAgICAwUDAwMDAwYEBAMFBwYHBwcGBwcICQsJCAgKCAcHCg0KCgsMDAwMBwkODw0MDgsMDAz/2wBDAQICAgMDAwYDAwYMCAcIDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAz/wAARCABJAFwDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD+f+iiigAooooAKKKKACiiigAooooAKKKKACiiigAoor0T9ln9mnXf2ufjLa+B/Dd3pNlq13p+o6kkupSyR24jsbGe+lBaNHbcYrdwvy4LFQSoJYHRy6JNv0Su38kgPO6KKKACivRPA/7NOu+P/wBnDx98ULO70mPQPh1qGk6bqVvNLILyeTUTciAwqEKMq/ZZN+51I3LgNk487oeknF7q34pNfg0/mAUUUUAFFFFABRRRQAV9q/8ABAv4ueLPhr/wUFsrPwz4m8Q6BFr3hfxLHdwaZqM1quovFoOozWyyLGw8wpOsbxg52yKrLhgDXxVWr4H8da38MfF+neIPDesar4e1/R51urDUtMu5LS8sZlOVkiljIdHB6MpBFNP3ZR25oyjftzRcb/K9xP0v/wAA/Rj9mr45J4a/4JqeIfjJqPxp+OHgz4peK/iU+jeNvH3hDSF8R+J5LRbCCXT7S5vZ9VsZ7W3mdbl8pI4uHtlV+IUFbaft7fDyy/aV+J2o+HtO+Pnwht/jHaeGLZ/ir4X8PwaF4m0bWfsHmTO1jb3DLJY6rMUvpbeC9ikl2LIDLtUH4G8K/ttfGfwJ8Udc8caJ8XPido3jTxMgj1jxBY+Kb631TVlG0hbi5SUSyj5E4dj91fQVH8P/ANtD4xfCbxx4i8TeFvix8S/DXiTxfKZ9e1bSvE97Z32tyF2cvdTRyq87F3dsyFjliepNUprn5mtLR0Tta0YxaT3SfLzXXLZ2upW1nlag4p63er63k5Xa2utI630uk430++dS+JXxr/Y9/Y6/bm8A/wDC3vEp1nwJ8SfD9lNdeGNZuNOsQ11dasmoSQQQtGtulw4iE0aqoLKqODtAr8u67H4UftD+P/gNqOq3ngbxz4w8GXeu2rWOpT6FrNzp0mo27HLQzNC6mSMkAlWyCe1cdXPTpuLvJ3doLa3wwUNl092/k21bS73qzUpPl0V2183f7/8ALcKKKK1MwooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooA//2Q==","relevant_Currency1":"BTC","relevant_Currency2":null,"relevant_Currency5":null,"relevant_Currency4":null,"relevant_Currency10":null,"relevant_Currency9":null,"relevant_Currency3":null,"relevant_Currency6":null,"relevant_Currency8":null,"relevant_Currency7":null},{"id":13,"date":"2022-05-14T04:29:05.926+00:00","title":"標題","contentOfNews":"內容","imageOfNews":"data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAIBAQIBAQICAgICAgICAwUDAwMDAwYEBAMFBwYHBwcGBwcICQsJCAgKCAcHCg0KCgsMDAwMBwkODw0MDgsMDAz/2wBDAQICAgMDAwYDAwYMCAcIDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAz/wAARCABJAFwDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD+f+iiigAooooAKKKKACiiigAooooAKKKKACiiigAoor0T9ln9mnXf2ufjLa+B/Dd3pNlq13p+o6kkupSyR24jsbGe+lBaNHbcYrdwvy4LFQSoJYHRy6JNv0Su38kgPO6KKKACivRPA/7NOu+P/wBnDx98ULO70mPQPh1qGk6bqVvNLILyeTUTciAwqEKMq/ZZN+51I3LgNk487oeknF7q34pNfg0/mAUUUUAFFFFABRRRQAV9q/8ABAv4ueLPhr/wUFsrPwz4m8Q6BFr3hfxLHdwaZqM1quovFoOozWyyLGw8wpOsbxg52yKrLhgDXxVWr4H8da38MfF+neIPDesar4e1/R51urDUtMu5LS8sZlOVkiljIdHB6MpBFNP3ZR25oyjftzRcb/K9xP0v/wAA/Rj9mr45J4a/4JqeIfjJqPxp+OHgz4peK/iU+jeNvH3hDSF8R+J5LRbCCXT7S5vZ9VsZ7W3mdbl8pI4uHtlV+IUFbaft7fDyy/aV+J2o+HtO+Pnwht/jHaeGLZ/ir4X8PwaF4m0bWfsHmTO1jb3DLJY6rMUvpbeC9ikl2LIDLtUH4G8K/ttfGfwJ8Udc8caJ8XPido3jTxMgj1jxBY+Kb631TVlG0hbi5SUSyj5E4dj91fQVH8P/ANtD4xfCbxx4i8TeFvix8S/DXiTxfKZ9e1bSvE97Z32tyF2cvdTRyq87F3dsyFjliepNUprn5mtLR0Tta0YxaT3SfLzXXLZ2upW1nlag4p63er63k5Xa2utI630uk430++dS+JXxr/Y9/Y6/bm8A/wDC3vEp1nwJ8SfD9lNdeGNZuNOsQ11dasmoSQQQtGtulw4iE0aqoLKqODtAr8u67H4UftD+P/gNqOq3ngbxz4w8GXeu2rWOpT6FrNzp0mo27HLQzNC6mSMkAlWyCe1cdXPTpuLvJ3doLa3wwUNl092/k21bS73qzUpPl0V2183f7/8ALcKKKK1MwooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooA//2Q==","relevant_Currency1":"BTC","relevant_Currency2":"ETH","relevant_Currency5":null,"relevant_Currency4":null,"relevant_Currency10":null,"relevant_Currency9":null,"relevant_Currency3":null,"relevant_Currency6":null,"relevant_Currency8":null,"relevant_Currency7":null},{"id":12,"date":"2022-05-14T04:29:05.233+00:00","title":"標題","contentOfNews":"內容","imageOfNews":"data:image/jpeg;base64,/9j/4AAQSkZJRgABAQEAYABgAAD/2wBDAAIBAQIBAQICAgICAgICAwUDAwMDAwYEBAMFBwYHBwcGBwcICQsJCAgKCAcHCg0KCgsMDAwMBwkODw0MDgsMDAz/2wBDAQICAgMDAwYDAwYMCAcIDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAz/wAARCABJAFwDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD+f+iiigAooooAKKKKACiiigAooooAKKKKACiiigAoor0T9ln9mnXf2ufjLa+B/Dd3pNlq13p+o6kkupSyR24jsbGe+lBaNHbcYrdwvy4LFQSoJYHRy6JNv0Su38kgPO6KKKACivRPA/7NOu+P/wBnDx98ULO70mPQPh1qGk6bqVvNLILyeTUTciAwqEKMq/ZZN+51I3LgNk487oeknF7q34pNfg0/mAUUUUAFFFFABRRRQAV9q/8ABAv4ueLPhr/wUFsrPwz4m8Q6BFr3hfxLHdwaZqM1quovFoOozWyyLGw8wpOsbxg52yKrLhgDXxVWr4H8da38MfF+neIPDesar4e1/R51urDUtMu5LS8sZlOVkiljIdHB6MpBFNP3ZR25oyjftzRcb/K9xP0v/wAA/Rj9mr45J4a/4JqeIfjJqPxp+OHgz4peK/iU+jeNvH3hDSF8R+J5LRbCCXT7S5vZ9VsZ7W3mdbl8pI4uHtlV+IUFbaft7fDyy/aV+J2o+HtO+Pnwht/jHaeGLZ/ir4X8PwaF4m0bWfsHmTO1jb3DLJY6rMUvpbeC9ikl2LIDLtUH4G8K/ttfGfwJ8Udc8caJ8XPido3jTxMgj1jxBY+Kb631TVlG0hbi5SUSyj5E4dj91fQVH8P/ANtD4xfCbxx4i8TeFvix8S/DXiTxfKZ9e1bSvE97Z32tyF2cvdTRyq87F3dsyFjliepNUprn5mtLR0Tta0YxaT3SfLzXXLZ2upW1nlag4p63er63k5Xa2utI630uk430++dS+JXxr/Y9/Y6/bm8A/wDC3vEp1nwJ8SfD9lNdeGNZuNOsQ11dasmoSQQQtGtulw4iE0aqoLKqODtAr8u67H4UftD+P/gNqOq3ngbxz4w8GXeu2rWOpT6FrNzp0mo27HLQzNC6mSMkAlWyCe1cdXPTpuLvJ3doLa3wwUNl092/k21bS73qzUpPl0V2183f7/8ALcKKKK1MwooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooA//2Q==","relevant_Currency1":"BTC","relevant_Currency2":"ETH","relevant_Currency5":null,"relevant_Currency4":null,"relevant_Currency10":null,"relevant_Currency9":null,"relevant_Currency3":null,"relevant_Currency6":null,"relevant_Currency8":null,"relevant_Currency7":null}]
 ```

網頁則是這樣
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
    <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
        <!DOCTYPE html>
        <html>

        <head>
            <meta charset="UTF-8">
            <title>fetch測試</title>
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
                    fetch("http://localhost:8080/myapp/news/get?currencyName=BTC").then(function(response) {
                        return response.json();
                    }).then(function(array) {
                        $.each(array, function(index, value) {
                            $("#test").append(`id:` + value.id).append(`<br>Title:` + value.title + `<br>`)
                        })



                    })
                })
            </script>

        </body>

        </html>
```
網頁呈現起來會像是這樣





