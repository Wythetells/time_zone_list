

ajax调用示例：

```html

<!----调用时区列表----------->
<input class="form-control" list="time_zone_list" type="text" name="time_zone" required="" id="time_zone" style="width:196px">
<!-----------时区列表---------------------------->
<datalist id="time_zone_list">
</datalist>
    
    
    
<script>
    
time_zone_list_url= './time_zone_list.html';
  
function get_data_list(url,list_id) {
    //1.创建ajax对象
    var oAjax = null
    //此处必须需要使用window.的方式,表示为window对象的一个属性.不存在是值为undefined,进入else/若直接使用XMLHttpRequest在不支持的情况下会报错
    if (window.XMLHttpRequest) {
        oAjax = new XMLHttpRequest();
    } else {
        //IE6以上,现在应该不需要考虑IE6了
        oAjax = new ActiveXObject("Microsoft.XMLHTTP");
    }
    //2.连接服务器
    //open(方法,url,是否异步)
    oAjax.open("GET", url, true);
    //3.发送请求
    oAjax.send(null);
    //4.接收返回
    //OnRedayStateChange事件
    oAjax.onreadystatechange = function () {
        if (oAjax.readyState === 4) {
			//window.alert(oAjax.status );
            if (oAjax.status === 200) {
                document.getElementById(list_id).innerHTML=oAjax.responseText;
            } else {
                window.alert('列表拉取失败，error: '+oAjax.status+'\n');
            }
        }
    };
}

get_data_list(time_zone_list_url,'time_zone_list')
</script>

```

