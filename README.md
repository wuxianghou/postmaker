# postmaker
自动生成微信带二维码推广海报。

这几天一个小项目，需要做一个自动生成带用户推广二维码的海报的功能。技术人员搞了几天，没有高出了，说没有找到现成的轮子。于是操起了好久没有写程序的手
自己造了一个小轮子。

这个轮子根据固定的海报格式自动生成推广海报。

# 原理

一般的推广活动的海报样式都一样，需要改变的只是用户的头像，昵称，以及用户的推广二维码。所以只需要做好海报背景图片，然后根据不同用户的个人信息生成对应用户的
推广海报即可。

## 输入信息参数

  输入参数：
	1. 海报背景图片（720,1280）
	2. 用户头像图片（正方形，最后缩放为（88,88））
	3. 用户昵称
	4. 二维码图片（正方形，最后缩放为（142,142））
	5. 文字颜色
  
# 示例
'''python
if __name__=='__main__':
	backImg = r".\20170815112219.jpg"
	font = r".\msyh.ttc"
	pMaker = postMaker(backImg=backImg, font= font)
	userIcon = r'.\testIcon.jpg'
	qrImg = r'.\qrimg.jpg'
	pMaker.create(
		userIcon=userIcon,
		userName=U"武妝妝",
		qrImg=qrImg,
		textColor={'R':0,'G':0,'B':0})
	print 'ok'
'''
# 生成海报示例
![Aaron Swartz](https://raw.githubusercontent.com/wuxianghou/postmaker/master/testPost.jpg)
# API

为了方便大家使用，我把这个功能部署了一个示例，大家可以在需要的时候调用，试试。

## API 地址
http://openapi.nanchangmama.com/make_post/

## 参数格式 （JSON）

{
'userName': '武妝妝', 
'userAvatar': 'http://static.dryeam.com/testIcon.jpg',
'qrImg': 'http://static.dryeam.com/qrimg.jpg', 
'backGroundImg': 'http://static.dryeam.com/20170815112219.jpg', 
'textColor': {'B': 45, 'R': 123, 'G': 9}
}

## 调用示例
from PIL import Image
from StringIO import StringIO
import requests

para = {'userName': '武妝妝', 'userAvatar': 'http://static.dryeam.com/testIcon.jpg', 'qrImg': 'http://static.dryeam.com/qrimg.jpg', 'backGroundImg': 'http://static.dryeam.com/20170815112219.jpg', 'textColor': {'B': 45, 'R': 123, 'G': 9}}

r = requests.post("http://openapi.nanchangmama.com/make_post/",data=json.dumps(para))

result = Image.open(StringIO(r.content))
result.show()





