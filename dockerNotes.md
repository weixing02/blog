# Some Docker Notes

---

1. ```docker run -i -t``是常用的组合命令，其中```-i```表示以交互模式运行容器，```-t```表示为容器重新分配一个伪输入终端，可以尝试只使用```-i```或者```-t```，前者虽然具有交互性，但是并没有启动一个新的伪终端，看不见容器中系统的样子，类似于在系统中盲人摸象；后者虽然启动了一个伪终端，但是却缺乏交互性，输入命令无效。

2. ```docker run /bin/bash```的作用是在容器中启动```bash```，因为容器中如果没有一个进程在运行的话就会自动退出

3. ```docker exec -it container_id /bin/bash``` 和```docker attach```的区别在于，```Docker attach```必须是登陆到一个已经运行的容器里。需要注意的是如果从这个容器中exit退出的话，就会导致容器停止！而```docker exec```在容器中exit会发现容器还在运行。

4. 对于一个已关闭的容器，可以使用```docker start -ai container```来登陆，其实过程就是先启动容器，然后再进入容器内。
