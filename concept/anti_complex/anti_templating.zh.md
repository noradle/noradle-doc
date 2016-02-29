使用页面模板的问题
------------------------------

* HTML 页面中包含了代码，代码中又输出 HTML 内容，概念上或理解上就增加了复杂性，范例如：
  - marker like `<% ... %>` to mark code
  - print html in code like `<?php echo '<p>Hello World</p>'; ?>`

Noradle 关于带入数据生成页面的设计理念

* 生成页面的存储过程就是标准的 plsql 代码，简单直接
* 没有模板就没有将模板编译成宿主语言的过程
* plsql代码直接向http响应输入内容
* 输入API中直接写 html 代码，但是可以使用简写，[参考](https://github.com/noradle/plsql-print/wiki)，特别是[o(ztag) API](https://github.com/noradle/plsql-print/wiki/API-o-ztag)

以下举例说明各种语言和web架构下使用页面模板的问题点

### a noradle plsql servlet example

```plsql
procedure bind_data is
  cursor c_packages is
    select *
      from user_objects a
     where a.object_type = 'PACKAGE'
       and rownum <= 5
     order by a.object_name asc;
begin
  b.l('<!DOCTYPE html>');
  o.t('<html>');
  o.t('<body>');
  o.t('<table rules=all cellspacing=0 cellpadding=5 style="border:1px solid silver;">');
  o.t(' <caption>', 'bind sql data to table example');
  o.t(' <thead>', o.t('<tr>', m.w('<th>@</th>', 'package name,created')));
  o.t(' <tbody>');
  for i in c_packages loop
    o.t('<tr>');
    o.t(' <td>', i.object_name);
    o.t(' <td>', t.d2s(i.created));
    o.t('</tr>');
  end loop;
  o.t(' </tbody>');
  o.t('</table>');
  o.t('</body>');
  o.t('</html>');
end;
```

### a ruby example

```ruby
<%= form_for :article do |f| %>
  <p>
    <%= f.label :title %><br>
    <%= f.text_field :title %>
  </p>

  <p>
    <%= f.label :text %><br>
    <%= f.text_area :text %>
  </p>

  <p>
    <%= f.submit %>
  </p>
<% end %>
```

remarks:

* 创造了自己的语法，f.label, f.text_field 等等，重复造轮子
* 讨厌丑陋的 `<%= expression %> 和 <% statement %>`
