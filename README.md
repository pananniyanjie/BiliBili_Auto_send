# B站自动发弹幕

#### 介绍
采用添加随机字母后缀来骗过b站检测机制，

待开发：
1.随机复读
2.随机时间
3.随机加入无关句子
#### 使用方法
按F12进入浏览器控制台并添加这段代码
#### 软件代码
var event = document.createEvent('Event');
var StrA;
var StrB;

event.initEvent('input', true, true);
function genEnCode(length, hasNum, hasChar, hasSymbol, caseSense, lowerCase) {
    var m = "";
    if (hasNum == "0" && hasChar == "0" && hasSymbol == "0") return m;
    for (var i = length; i >= 0; i--) {
        var num = Math.floor((Math.random() * 94) + 33);
        if (
            (
                (hasNum == "0") && ((num >= 48) && (num <= 57))
            ) || (
                (hasChar == "0") && ((
                    (num >= 65) && (num <= 90)
                ) || (
                    (num >= 97) && (num <= 122)
                ))
            ) || (
                (hasSymbol == "0") && ((
                    (num >= 33) && (num <= 47)
                ) || (
                    (num >= 58) && (num <= 64)
                ) || (
                    (num >= 91) && (num <= 96)
                ) || (
                    (num >= 123) && (num <= 127)
                ))
            )
        ) {
            i++;
            continue;
        }
        m += String.fromCharCode(num);
    }
    if(caseSense == "0"){
        m = (lowerCase == "0")?m.toUpperCase():m.toLowerCase();
    }
    return m;
}
function fun123(){
    StrA = "前方高能";
     StrB = genEnCode(1, 1, 1, 1, 1, 1);
    $('.chat-input.border-box').val(StrA + StrB);
    $('.chat-input.border-box')[0].dispatchEvent(event);
    $('.bl-button.live-skin-highlight-button-bg.bl-button--primary.bl-button--small').click();
}
setInterval("fun123()","500");