# Homebrew安装指定版本的Formula

## 以安装```clang-format 3.8```为例

### 问题描述

由于```pre-commit```工具要求本机安装```clang-format```版本为```3.8```，但是在直接使用```brew install clang-format```时，```brew```首先会进行自身的更新，执行```brew update```，然后安装最新版本的```clang-format```，使用```clang-format```查看版本会发现此时的```clang-format```版本为```7.0.0```，那么要安装```clang-format 3.8```版本应该怎么做呢？

### 理解Homebrew的Formula的安装形式

Homebrew是基于git进行版本管理的，目前最新的最全的Homebrew库是```Homebrew/homebrew-core```，对于每一个Formula都维护一个```.rb```文件，例如```clang-format.rb```文件，这个文件的路径是

```$(brew --prefix)/Homebrew/Library/Taps/homebrew/homebrew-core/Formula```

Formula文件夹下存放了各个Formula的```.rb```文件，那么这个文件有什么用呢？例如我们在执行```brew install clang-format```的时候会根据```clang-format.rb```的文件内容按步骤下载相应的依赖，并安装```clang-format```，也就是说```clang-format```的安装是完全依赖于```clang-format.rb```文件的。

有了上面的理解，我们就可以发现，如果要安装旧版本的```clang-format```，就只需要通过git操作来回滚```clang-format.rb```到旧的版本，之后再重新执行```brew install clang-format```即可。

有些Formula维护的很好，可以通过```git log -S"版本号" Formula```来查看相应的commit编码，这样一来，回滚操作就十分方便了。
