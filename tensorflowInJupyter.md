1. 打开终端
2. 运行下面的命令来启用TensorFlow 
```
source activate tensorflow
```
3. 现在我们已经进入了TensorFlow的环境，我们要在这个环境中安装```iPython```和```jupyter```，运行下面的命令
```
conda install ipython
conda install jupyter
```
4. 首先运行下面的命令

```
ipython kernelspec install-self --user
```

我这里得到的结果是

```
Installed kernelspec python3 in /Users/charliebrummitt/Library/Jupyter/kernels/python3
```
5. 运行下边的命令
```
mkdir -p ~/.ipython/kernels 
```

6. 然后运行下边的命令，使用你选择的名字来代替<kernel_name>（我使用的tfkernel），并且使用第4步中得到的路径(例如，
```
~/.local/share/jupyter/kernels/pythonX)
```
来替换下方命令中的第一个路径。
```
mv ~/.local/share/jupyter/kernels/pythonX ~/.ipython/kernels/<kernel_name>
```
7. 现在，打开Jupyter Notebook，选择```Kernel -> Change kernel```，你将看到一个新的kernel。但是，新的kernel与你之前的kernel拥有相同点名字，运行下边的命令，给你的新kernel起一个不同的名字。
```
cd ~/.ipython/kernels/tfkernel/
vim kernel.json
```

将"display_name"中的默认值Python 3替换为你的新名字，然后保存，并退出。
8. 打开一个新的Jupyter Notebook，输入一行```import tensorflow as tf```并运行，如果没有出现任何错误，那么就搞定了
