## h5手机端调起输入法时隐藏底部导航
```
<script>
    let oHeight = $(window).height(); //浏览器当前的高度
    $(window).resize(function(){
        if($(window).height() < oHeight){
            $('.footer_div').css('display', 'none');
        }else{
            $('.footer_div').css('display', 'block');
        }
    });
</script>
```