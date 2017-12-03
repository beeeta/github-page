Title: wtf表单处理
Category: python_web
Date: 2017-12

### 使用方法
- 创建表单

```python

from flask_wtf import Form
from wtforms import TextField
from wtforms.validators import DataRequired

class MyForm(Form):
    username = TextField('username', validators=[DataRequired()])
    upload = FileField('image', validators=[
        FileRequired(),
        FileAllowed(['jpg', 'png'], 'Images only!')
    ])

```

- 生成表单
```python
@app.route('/login')
def login():
	return render_template('login.html',form=MyForm())

```
- 定义表单字段

```
<form>

{{form.hidden_tag()}} # 这里是csrf_token字段
<input type=text name='username'/> # username 对应MyForm对象中的字段，在提交表单时，值会进行自动绑定

</form>

```

- 处理提交的表单

```
@app.route('/submit', methods=('GET', 'POST'))
def submit():
    form = MyForm()
    if form.validate_on_submit():
	# 处理表单信息 form.data
        return redirect('/success')
    return render_template('submit.html', form=form)

```

- ajax的csrf消息头
在页面的meta或者脚本中初始化csrf_token的值：
```
<meta name="csrf-token" content="{{ csrf_token() }}">

<script type="text/javascript">
    var csrftoken = "{{ csrf_token() }}"
</script>

```
然后在ajax请求中设置共用消息头：
```
var csrftoken = $('meta[name=csrf-token]').attr('content')

$.ajaxSetup({
    beforeSend: function(xhr, settings) {
        if (!/^(GET|HEAD|OPTIONS|TRACE)$/i.test(settings.type)) {
            xhr.setRequestHeader("X-CSRFToken", csrftoken)
        }
    }
})

```







