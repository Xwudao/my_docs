# Laravel Use

## 帮助函数

### Utils

```php
<?php


namespace App\helper;


class Utils
{
    public static function res($msg, $code = 1, ...$data)
    {
        return json_encode(compact('msg', 'code', 'data'));
    }
}
```



### 配置转数组

```php
function get_settings(array $old_settings): array
{
    $new_settings = [];
    foreach ($old_settings as $setting) {
        $new_settings[$setting['name']] = $setting['value'];
    }
    return $new_settings;
}
```

### 大力盘获取密码

```php
function get_pass_from_dali($disk_id)
{
    $curl = new Curl();
    $url = 'https://helper.aisouziyuan.com/Extensions/Api/ResourcesCode?v=2.532';
    $json = ['url' => $disk_id, 'wrong' => false, 'type' => 'baidu', 'v' => '2.532'];
    $curl->setHeader('Content-Type', 'application/json');
    $curl->setUserAgent('Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/77.0.3865.120 Safari/537.36');
    $curl->setOpts([CURLOPT_SSL_VERIFYPEER => 0, CURLOPT_SSL_VERIFYHOST => 0]);
    // $curl->setProxy('127.0.0.1:8888');
    $curl->post($url, json_encode($json));
    $res = $curl->response;
    if ($res) {
        return $res;
    } else {
        return '';
    }
}
```

### 云盘精灵获取密码

```php
function get_yunpanjingling_pass($disk_id)
{
    $curl = new Curl();
    $url = 'https://ypsuperkey.meek.com.cn/api/v1/items/BDY-' . $disk_id . '?client_version=2018.10';
    // 伪造客户端来源IP
    $fake_ip = rand(1, 254) . "." . rand(1, 254) . "." . rand(1, 254) . "." . rand(1, 254);
    // curl_setopt ($ch, CURLOPT_HTTPHEADER, array('CLIENT-IP:'.$xforip, 'X-FORWARDED-FOR:'.$xforip));
    $curl->setHeader('CLIENT-IP', $fake_ip);
    $curl->setHeader('X-FORWARDED-FOR', $fake_ip);
    $curl->setOpts([CURLOPT_SSL_VERIFYPEER => 0, CURLOPT_SSL_VERIFYHOST => 0]);
    $curl->get($url);
    $res = $curl->rawResponse;
    Log::info('云盘精灵接口：' . $res);
    $data = json_decode($res, true);
    if (isset($data['access_code'])) {
        return $data['access_code'];
    } else {
        return '';
    }
}
```

### 分词

```php
function participle($words)
{
    $curl = new Curl();
    $curl->setOpts([CURLOPT_SSL_VERIFYPEER => 0, CURLOPT_SSL_VERIFYHOST => 0]);
    $curl->get('http://120.26.6.172/get.php?source=' . urlencode($words) . '&param1=0.6&param2=1&json=1');
    $res = $curl->rawResponse;

    $data = json_decode($res, true);
    $res_data = [];
    foreach ($data as $item) {
        array_push($res_data, $item['t']);
    }
    return $res_data;
}
```

### 友好时间显示

```php
function friendlyDate($sTime, $type = 'normal', $alt = 'false')
{
    if (!$sTime)
        return '';
    $sTime = is_numeric($sTime) ? $sTime : strtotime($sTime);
    //sTime=源时间，cTime=当前时间，dTime=时间差
    $cTime = time();
    $dTime = $cTime - $sTime;
    $dDay = intval(date("z", $cTime)) - intval(date("z", $sTime));
    //$dDay     =   intval($dTime/3600/24);
    $dYear = intval(date("Y", $cTime)) - intval(date("Y", $sTime));
    //normal：n秒前，n分钟前，n小时前，日期
    if ($type == 'normal') {
        if ($dTime < 60) {
            if ($dTime < 10) {
                return '刚刚';    //by yangjs
            } else {
                return intval(floor($dTime / 10) * 10) . "秒前";
            }
        } elseif ($dTime < 3600) {
            return intval($dTime / 60) . "分钟前";
            //今天的数据.年份相同.日期相同.
        } elseif ($dYear == 0 && $dDay == 0) {
            //return intval($dTime/3600)."小时前";
            return '今天' . date('H:i', $sTime);
        } elseif ($dYear == 0) {
            return date("m月d日 H:i", $sTime);
        } else {
            return date("Y-m-d H:i", $sTime);
        }
    } elseif ($type == 'mohu') {
        if ($dTime < 60) {
            return $dTime . "秒前";
        } elseif ($dTime < 3600) {
            return intval($dTime / 60) . "分钟前";
        } elseif ($dTime >= 3600 && $dDay == 0) {
            return intval($dTime / 3600) . "小时前";
        } elseif ($dDay > 0 && $dDay <= 7) {
            return intval($dDay) . "天前";
        } elseif ($dDay > 7 && $dDay <= 30) {
            return intval($dDay / 7) . '周前';
        } elseif ($dDay > 30) {
            return intval($dDay / 30) . '个月前';
        }
        //full: Y-m-d , H:i:s
    } elseif ($type == 'full') {
        return date("Y-m-d , H:i:s", $sTime);
    } elseif ($type == 'ymd') {
        return date("Y-m-d", $sTime);
    } else {
        if ($dTime < 60) {
            return $dTime . "秒前";
        } elseif ($dTime < 3600) {
            return intval($dTime / 60) . "分钟前";
        } elseif ($dTime >= 3600 && $dDay == 0) {
            return intval($dTime / 3600) . "小时前";
        } elseif ($dYear == 0) {
            return date("Y-m-d H:i:s", $sTime);
        } else {
            return date("Y-m-d H:i:s", $sTime);
        }
    }
    return '';
}
```

### 电脑还是手机

```php
function isMobile()
{
    // 如果有HTTP_X_WAP_PROFILE则一定是移动设备
    if (isset ($_SERVER['HTTP_X_WAP_PROFILE'])) {
        return TRUE;
    }
    // 如果via信息含有wap则一定是移动设备,部分服务商会屏蔽该信息
    if (isset ($_SERVER['HTTP_VIA'])) {
        return stristr($_SERVER['HTTP_VIA'], "wap") ? TRUE : FALSE;// 找不到为flase,否则为TRUE
    }
    // 判断手机发送的客户端标志,兼容性有待提高
    if (isset ($_SERVER['HTTP_USER_AGENT'])) {
        $clientKeywords = array(
            'mobile',
            'nokia',
            'sony',
            'ericsson',
            'mot',
            'samsung',
            'htc',
            'sgh',
            'lg',
            'sharp',
            'sie-',
            'philips',
            'panasonic',
            'alcatel',
            'lenovo',
            'iphone',
            'ipod',
            'blackberry',
            'meizu',
            'android',
            'netfront',
            'symbian',
            'ucweb',
            'windowsce',
            'palm',
            'operamini',
            'operamobi',
            'openwave',
            'nexusone',
            'cldc',
            'midp',
            'wap'
        );
        // 从HTTP_USER_AGENT中查找手机浏览器的关键字
        if (preg_match("/(" . implode('|', $clientKeywords) . ")/i", strtolower($_SERVER['HTTP_USER_AGENT']))) {
            return TRUE;
        }
    }
    if (isset ($_SERVER['HTTP_ACCEPT'])) { // 协议法，因为有可能不准确，放到最后判断
        // 如果只支持wml并且不支持html那一定是移动设备
        // 如果支持wml和html但是wml在html之前则是移动设备
        if ((strpos($_SERVER['HTTP_ACCEPT'], 'vnd.wap.wml') !== FALSE) && (strpos($_SERVER['HTTP_ACCEPT'], 'text/html') === FALSE || (strpos($_SERVER['HTTP_ACCEPT'], 'vnd.wap.wml') < strpos($_SERVER['HTTP_ACCEPT'], 'text/html')))) {
            return TRUE;
        }
    }
    return FALSE;

}
```

### 放大图片

```php
function resizeImage($srcImage, $per, $name)
{

    list($width, $height, $type, $attr) = getimagesize($srcImage);
    $maxWidth = $width * $per;
    $maxHeight = $height * $per;
    //    if($width < $maxWidth  || $height < $maxHeight) return ;
    switch ($type) {
        case 1:
            $img = imagecreatefromgif($srcImage);
            break;
        case 2:
            $img = imagecreatefromjpeg($srcImage);
            break;
        default:
            $img = imagecreatefrompng($srcImage);
            break;
    }
    $canvas = imagecreatetruecolor($maxWidth, $maxHeight); // 创建一个真彩色图像 我把它理解为创建了一个画布

    imagecopyresampled($canvas, $img, 0, 0, 0, 0, $maxWidth, $maxHeight, $width, $height);

    imagejpeg($canvas, $name, 100);
}
```

### 数字转换英语

```php
function transform_num_to_english($num): string
{
    // 只转换前3吧，其余返回other
    $res = [1 => 'first', 2 => 'second', 3 => 'third'];
    if (in_array($num, [1, 2, 3])) {
        return $res[$num];
    } else {
        return 'other';
    }

}
```

### 去除Markdown标签

```php
function strip_markdown_tags($str): string
{
    $preg = '/[\`\*\_\[\]\#\+\-\!\>]/';
    $new = preg_replace($preg, "", $str);
    // $new = strip_tags($new);
    // // laravel 中使用{!! !!} 就不用使用以下代码了
    // $new = htmlspecialchars($new);
    $old_arr = ['<', '>'];
    $new_arr = ['&lt;', '&gt;'];
    $new = str_replace($old_arr, $new_arr, $new);
    return $new;
}
```

### 解析Markdown目录

```php
function parseToc($html, &$toc)
{
    $encoding = '<?xml encoding="utf-8" ?' . '>';
    $doc = new \DOMDocument();
    $doc->loadHTML($encoding . $html);
    $xml = simplexml_import_dom($doc);
    $headings = $xml->xpath('//h1|//h2|//h3|//h4|//h5|//h6');
    $toc = [];
    foreach ($headings as $i => $heading) {
        $level = $heading->getName();
        $id = "toc-{$i}";
        $heading->addAttribute('id', $id);
        $toc[] = [
            'id' => $id,
            'level' => $level,
            'title' => strval($heading)
        ];
    }
    $resultHtml = '';
    foreach ($xml->body->children() as $child) {
        $resultHtml .= $child->asXML();
    }
    return $resultHtml;
}
```







## 前台

public资源下载：https://w-fille.oss-cn-beijing.aliyuncs.com/miaiyu-files/public.zip



## 后台

### 登录

#### html

```html
<div class="login-form ">
    <form action="{{ route('user.login') }}" method="post">
        @csrf

        <h3 class="text-center font-weight-bold">登录</h3>
        <div class="form-group">
            <label class="font-weight-bold" for="username">用户名：</label>
            <input type="text" name="username" class="form-control" id="username">
        </div>
        <div class="form-group">
            <label class="font-weight-bold" for="password">密码：</label>
            <input type="password" name="password" class="form-control" id="password">
        </div>
        <div class="custom-control custom-checkbox">
            <input type="checkbox" class="custom-control-input" name="remember" checked id="remain_me">
            <label class="custom-control-label" for="remain_me">记住我</label>
        </div>
        <div class="form-group mt-3 float-right clearfix">
            <button class="btn btn-primary">登录</button>
        </div>

    </form>
</div>
```

#### php

```php
$is_remember = $request['remember'] == 'on' ? true : false;
$login = Auth::attempt([
    'username' => $request['username'],
    'password' => $request['password'],
], $is_remember);

if ($login) {
    return redirect(route('admin.index'));
} else {
    return back()->with('error', '用户不存在，或密码错误。');
}
```

### 退出

```php
Auth::logout();return redirect(route('user.login.form'))->with('success', '退出成功');
```

### 修改密码

#### html

```html
<div class="card">
    <div class="card-body">
        <form action="{{ route('modify.pass') }}" method="post">
            @csrf
            <div class="form-group">
                <label for="old_password" class="font-weight-bold">旧密码</label>
                <input type="password" class="form-control" name="old_password" id="old_password">
            </div>
            <div class="form-group">
                <label for="password" class="font-weight-bold">新密码</label>
                <input type="password" class="form-control" name="password" id="password">
            </div>
            <div class="form-group">
                <label for="password_confirmation" class="font-weight-bold">确认密码</label>
                <input type="password" class="form-control" name="password_confirmation"
                       id="password_confirmation">
            </div>
            <div class="form-group">
                <button type="submit" class="btn btn-primary">修改</button>
            </div>
        </form>
    </div>
</div>
```

#### php

**request**

```php
/**
 * Determine if the user is authorized to make this request.
 *
 * @return bool
 */
public function authorize()
{
    return Auth::check();
}

public function addValidate()
{
    Validator::extend('check_pass', function ($attribute, $value, $parameters, $validator) {
        return Hash::check($value, Auth::user()->password);
    });
}

/**
 * Get the validation rules that apply to the request.
 *
 * @return array
 */
public function rules()
{
    $this->addValidate();
    return [
        'old_password' => 'required|check_pass',
        'password' => 'required|confirmed',
        'password_confirmation' => 'required',
    ];
}

public function messages()
{
    return [
        'password.required' => '新密码不能为空',
        'password_confirmation.required' => '确认密码不能为空',
        'old_password.required' => '旧密码不能为空',
        'old_password.check_pass' => '旧密码错误',
        'password.confirmed' => '两次新密码不一致',
    ];
}
```

**controller**

```php
$d = Auth::user()->update([
    'password' => bcrypt($request->password)
]);
if ($d) {
    Auth::logout();
    return redirect(route('user.login.form'))->with('success', '修改成功，请重新登录');
} else {
    return back()->with('error', '修改失败，请重试');
}
```



### 修改密码（自定义）

#### Php

```php
public function modify_pass(Request $request)
    {
        $old_pass = $request->post('old_password');
        $password_confirmation = $request->post('password_confirmation');
        $new_pass = $request->post('password');

        if (!$old_pass || !$password_confirmation || !$new_pass) {
            return Utils::res('所有项不能为空', 0);
        }
        $user = Auth::guard('owner')->user();
        if (!Hash::check($old_pass, $user->password)) {
            return Utils::res('你的原密码错误', 0);
        }
        if ($password_confirmation != $new_pass) {
            return Utils::res('新密码不一致', 0);
        }
        $user->password = bcrypt($new_pass);
        $user->save();
        return Utils::res('修改成功', 1);
    }
```

#### Html

```html
<div class="card">
    <div class="card-body">
        <form action="#" method="post" onsubmit="return false;">
            <div class="form-group">
                <label for="old_password" class="font-weight-bold">旧密码</label>
                <input type="password" class="form-control" name="old_password"
                       id="old_password">
            </div>
            <div class="form-group">
                <label for="password" class="font-weight-bold">新密码</label>
                <input type="password" class="form-control" name="password"
                       id="new_password" aria-label="new_password">
            </div>
            <div class="form-group">
                <label for="password_confirmation"
                       class="font-weight-bold">确认密码</label>
                <input type="password" class="form-control"
                       name="password_confirmation"
                       id="password_confirmation">
            </div>
            <div class="form-group">
                <button type="submit" id="btn_modify_pass" class="btn btn-primary">
                    修改密码
                </button>
            </div>
        </form>
    </div>
</div>
```

#### JavaScript

```javascript
// modify pass
let btn_modify_pass = $("#btn_modify_pass");
let input_old_pass = $("#old_password");
let input_confirmation_pass = $("#password_confirmation");
let input_new_pass = $("#new_password");

btn_modify_pass.click(function () {
    if (input_confirmation_pass.val() === '' || input_new_pass.val() === '' || input_old_pass.val() === '') {
        swal({text: '所有项不能为空', icon: 'info', button: false, timer: 1000});
        return;
    }

    axios.post('/owner/modify_pass', {
        old_password: input_old_pass.val(),
        password_confirmation: input_confirmation_pass.val(),
        password: input_new_pass.val()
    }).then(res => {
        let data = res.data;
        let icon = data.code === 1 ? 'success' : 'error';
        swal({text: data.msg, icon: icon, button: false, timer: 1000});
        console.log(res);
    }).catch(err => {
        swal({text: '系统错误，请稍后重试', icon: 'info', button: false, timer: 1000});
        console.log(err);
    })

});
```

### Ajax增加

#### 侧边html

```html
<div class="form">
    <div class="form-group">
        <label for="name" class="font-weight-bold">名称：</label>
        <input type="text" id="name" aria-label="name" name="name"
               placeholder="名称随意即可"
               class="form-control">
    </div>
    <div class="form-group">
        <label for="type" class="font-weight-bold">类型：</label>
        <input type="text" id="type" aria-label="type" name="type"
               placeholder="要填写真实类型"
               class="form-control">
    </div>
    <div class="form-group">
        <label for="content" class="font-weight-bold">回复内容：</label>
        <textarea name="content" id="content" cols="20" rows="8"
                  placeholder="内容随意即可"
                  class="form-control"></textarea>
    </div>
    <div class="form-group">
        <button class="btn btn-primary one">增加</button>
    </div>
</div>
```

#### Javascript

```php
// create
let name = $("#name");
let type = $("#type");
let content = $("#content");
let btn = $("#create");

function storeOrUpdate(name,type,content) {
    if (name!== '' && type !== '' && content !== '') {
        axios.post('./events', {
            name: name,
            type: type,
            content: content,
        }).then(res => {
            let data = res.data;
            if (data.code === 1) {
                swal({text: data.msg, timer: 1000, icon: 'success', button: false});
                setTimeout(function () {
                    location.reload();
                }, 1000);
            } else {
                swal({text: data.msg, timer: 1000, icon: 'error', button: false});
            }
        }).catch(err => {
            console.log(err);
            swal({text: '系统错误!', timer: 1000, icon: 'error', button: false});
        })
    } else {
        swal({text: '请输入完整的内容', timer: 1000, icon: 'info', button: false});
    }
}
btn.click(function () {
    storeOrUpdate(name.val(), type.val(), content.val());
});
```

#### Php

**store方法**

```php
$name = $request->post('name', '');
$type = $request->post('type', '');
$content = $request->post('content', '');

if ($name == '' || $type == '' || $content == '') {
    return Utils::res('输入不完整', 0);
} else {
    $old = EventReply::where('type', $type)->first();
    if ($old) {
        $old->update($request->all());
        return Utils::res('修改成功', 1);
    }
    EventReply::firstOrCreate($request->all());
    return Utils::res('创建成功', 1);
}
```

### Ajax删除

**html中，需要类似下面：**

```html
<a href="javascript:" data-id="{{ $event->id }}"
   id="del-{{ $event->id }}"
   class="btn btn-sm btn-danger">删除</a>
```

#### Php

```php
$item = EventReply::find($id);
if (!$item) {
    return Utils::res('数据库无此数据，可能已删除！', 0);
}
$d = $item->delete();
if ($d) {
    return Utils::res('删除成功', 1);
} else {
    return Utils::res('删除失败', 0);
}
```

#### JavaScript

```javascript
let btn_delete = $("[id^='del-']");
//delete
btn_delete.click(function () {
    let id = $(this).data('id');
    //
    swal({
        title: "确定删除吗？",
        text: "删除不可逆！",
        icon: "warning",
        buttons: ["取消","确定"],
        dangerMode: true,
    })
        .then((willDelete) => {
            if (willDelete) {
                axios.delete('./navImage/' + id).then(res => {
                    console.log(res);
                    let data = res.data;
                    let icon = data.code === 1 ? 'success' : 'error';
                    swal({text: data.msg, icon: icon, button: false, timer: 1000});
                    if (data.code === 1) {
                        setTimeout('location.reload()', 1000);
                    }
                }).catch(err => {
                    console.log(err);
                    swal({text: '请求错误!', timer: 1000, icon: 'error', button: false});
                })
            }
        });
});
```

### Ajax修改

#### JavaScript

```javascript
// modify
$("[id^='modify-']").click(function () {
    let m_name = $(this).data('name');
    let m_type = $(this).data('type');
    let m_content = $(this).data('content');

    name.val(m_name);
    type.val(m_type);
    content.val(m_content);
});
```

#### Php

**修改这里还是利用了store方法，增加了一个判断，若存在则是修改**

```php
$name = $request->post('name', '');
$type = $request->post('type', '');
$content = $request->post('content', '');

if ($name == '' || $type == '' || $content == '') {
    return Utils::res('输入不完整', 0);
} else {
    $old = EventReply::where('type', $type)->first();
    if ($old) {
        $old->update($request->all());
        return Utils::res('修改成功', 1);
    }
    EventReply::firstOrCreate($request->all());
    return Utils::res('创建成功', 1);
}
```

### 上传文件

**config目录新建配置文件：upload.php**

```php
<?php
/**
 * 配置上传文件的路径
 */
return [
    'upload_img_path' => 'app/public/img',
];

```

**在config/filesystems.php下定义**

在disks数组下，添加：

```php
'upload_img' => [
    'driver'=>'local',
    'root'=>storage_path(config('upload.upload_img_path')) // 这里的键值就是上面config目录定义的
],
```

对于想上传到public目录下，就使用`public_path()`帮助函数

**处理参考代码**

```php
$image = $request->file('image');
$title = $request->post('title');
$desc = $request->post('desc');
if (!$image || !$title || !$desc) {
    return back()->with('error', '抱歉，输入不完整');
}
// $t = $image->store(storage_path());
// dd($t);
$ext = $image->getClientOriginalExtension();
$path = $image->getRealPath();
$filename = 'upload/' . date("Y-m-d") . '_' . uniqid() . '.' . $ext;
Storage::disk('upload_img')->put($filename, file_get_contents($path));

$upload_path = $filename;
NavImage::create(compact('title', 'desc', 'upload_path'));
return back()->with('success', '添加成功');
```