---
layout: post
title: "bootstrap modal如何传值进modal框"
date: 2016-09-12 15:07:00
categories: ['bootstrap']
tags: ['bootstrap']
---
# [本文资料参考链接](http://www.juzi89.com/?p=127)
```
<a href="#myModal" role="button" data-toggle="modal" class="del" date-id="参数"><i class="icon-remove"></i></a>
```

```
<div class="modal small hide fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
    <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-hidden="true">×</button>
        <h3 id="myModalLabel">删除提示</h3>
    </div>
    <div class="modal-body">
        <p class="error-text"><i class="icon-warning-sign modal-icon"></i>确定要删除此项?</p>
    </div>
    <div class="modal-footer">
        <button class="btn" data-dismiss="modal" aria-hidden="true">关闭</button>
        <button class="btn btn-danger" data-dismiss="modal" date-id="需要传值的地方">删除</button>
    </div>
</div>
```
```
<script type="text/javascript">
    $(document).ready(function(){
        $(".del").click(function(){
            var id = $(this).attr('date-id');
            $("#myModal .modal-footer .btn-danger").attr("date-id",id);
            $("#Modal").modal();
        });
    });
</script>
```