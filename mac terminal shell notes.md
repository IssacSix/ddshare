## Some notes about mac terminal

1. 全部命令指南查找

   ```
   man ls
   ```

   ​

2. 查看当前位置：

   ```
   pwd
   ```

   ​

3. 命令文件的路径，返回执行某个命令时使用的哪个文件

   ```
   which nginx
   ```

   ​

4. 显示当前目录下的文件

   ```
   ls -l // 显示当前目录下文件的详细信息（大小、时间）
   ls -a // 显示全部文件 包含隐藏文件
   ```

   ​

5. 目录结构符

   ```
   ~	// 用户主目录
   /	// 根目录
   ./	// 当前目录
   ../ // 上级目录
   ```

   ​

6. 创建

   ```
   mkdir // 创建文件夹
   touch // 创建单个文件
   touch ~/desktop/test/ding/index.html
   mkdir -p ~/desktop/test2/ding/index2.html
   ```

   添加参数 -p 根据命令自动创建相应目录文件夹及文件

   ​

7. move

   ```
   mv 源 目标
   mv ~/desktop/test/ding/index.html ~/desktop/test2/ding/
   ```

   ​

8. copy

   ```
   cp 源 目标
   cp -r ~/desktop/test2/ding/index.html ~/desktop/test/ding/
   ```

   ​

9. 本地文件与服务器之前的传输

   ```
   scp

   1. 本地文件传输到服务器
   scp /Users/mac_pc/Desktop/test.png root@192.168.1.1:/root
   scp【本地文件的路径】【服务器用户名】@【服务器地址】：【服务器上存放文件的路径】

   2. 本地文件夹传输到服务器
   sup -r /Users/mac_pc/Desktop/test root@192.168.1.1:/root
   scp -r【本地文件的路径】【服务器用户名】@【服务器地址】：【服务器上存放文件的路径】

   3. 服务器上的文件传输到本地
   scp root@192.168.1.1:/data/wwwroot/default/111.png /Users/mac_pc/Desktop
   scp 【服务器用户名】@【服务器地址】：【服务器上存放文件的路径】【本地文件的路径】

   4. 服务器上的文件夹传输到本地
   sup -r root@192.168.1.1:/data/wwwroot/default/test /Users/mac_pc/Desktop
   scp -r 【服务器用户名】@【服务器地址】：【服务器上存放文件的路径】【本地文件的路径】
   ```

   ​

10. remove

    ```
    rm
    rm -rf ~/desktop/test ~/desktop/test2
    ```

    ​

11. 查找当前目录下文件

    ```
    find **/*.html
    ```

    ​

12. 打开文件夹

    ```
    open 打开的路径
    open ~/desktop/ding/
    open ~/desktop/ding -a sublime // sublime打开文件
    ```

    ​

13. 打印文件内容

    ```
    cat ~/desktop/test/ding/index.html
    ```

    ​

14. 清除: command + K



别的牛逼的命令我应该也是用不上，我所常用或者用过的命令，以上

























