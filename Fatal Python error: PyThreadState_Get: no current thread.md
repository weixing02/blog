## Fatal Python error: PyThreadState_Get: no current thread

---

当我们使用anaconda创建一个新的python环境，例如```conda create -n py2.7 python==2.7```，在这个环境中import一个第三方库时有可能发生这样的错误：

```
Fatal Python error: PyThreadState_Get: no current thread
```
例如在安装```paddlepaddle```时，我在尝试:

```
paddle.init(trainner_count=1, use_gpu=False)
```
时就报了上述错误，原因是什么呢？原因在也paddlepaddle安装后默认使用系统的python2.7而不是anaconda建立的新的python环境（尽管我们是在这个新环境下使用```pip install paddlepaddle```来安装的），我们先找到_swig_paddle.so的路径，我的anaconda路径是

```
sudo find ~/anaconda2/ _swig_paddle.so
```
发现全路径为:

```
/Users/starwe/anaconda2//lib/python2.7/site-packages/py_paddle/_swig_paddle.so
```

接下来使用```otool```来查找_swig_paddle.so的依赖项

```
otool -L /Users/starwe/anaconda2//lib/python2.7/site-packages/py_paddle/_swig_paddle.so
```

结果如下：

```
/System/Library/Frameworks/CoreFoundation.framework/Versions/A/CoreFoundation (compatibility version 150.0.0, current version 1445.12.0)
	/System/Library/Frameworks/Security.framework/Versions/A/Security (compatibility version 1.0.0, current version 58286.20.16)
	/usr/local/opt/python/Frameworks/Python.framework/Versions/2.7/Python (compatibility version 2.7.0, current version 2.7.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.0.0)
```
我们发现其中有一项是依赖系统的python2.7，那我们只需要把这行替换之后就可以解决问题啦，使用install_name_tool来替换路径:

```
install_name_tool -change /usr/local/opt/python/Frameworks/Python.framework/Versions/2.7/Python /Users/starwe/anaconda2//lib/libpython2.7.dylib /Users/starwe/anaconda2//lib/python2.7/site-packages/py_paddle/_swig_paddle.so
```

再使用otool来检查一下_swig_paddle.so的依赖项显示如下结果：

```
/System/Library/Frameworks/CoreFoundation.framework/Versions/A/CoreFoundation (compatibility version 150.0.0, current version 1445.12.0)
	/System/Library/Frameworks/Security.framework/Versions/A/Security (compatibility version 1.0.0, current version 58286.20.16)
	/Users/starwe/anaconda2//lib/libpython2.7.dylib (compatibility version 2.7.0, current version 2.7.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.0.0)
```

可以看到原来的依赖项已经被替换，现在再尝试运行
```
paddle.init()
```
就没问题了，mark!
