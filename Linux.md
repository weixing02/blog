#### sed

-n: silence模式；
-e: 直接在命令模式上进行sed进行编辑，默认-e
-f: 把sed命令写在一个文本文件中，使用-f filename，就可以直接调用file中的sed命令；
-i: 直接对文件进行修改，不输出到终端(mac下需要```sed -i "" '2,5d' test.txt```)

- 插入、增加：
a: 新增一行到指定行的下方；
i: 新增一行到指定行的上方；

- 替换：
c: 用一个字符串替换指定行；
s: 部分替换，可以接正则表达式；
正则表达式之后接```g```表示替换所有，否则只会替换某行中第一个匹配到的项；

- 删除：
d

- 打印：
p: 打印某些行，通常与```-n```一起使用，否则会输出对应的行再输出全部的内容；
