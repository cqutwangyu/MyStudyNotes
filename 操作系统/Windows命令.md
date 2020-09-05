1. `netstat  -anp  |grep  3306` 查看占用3306端口的进程的信息
2. `taskkill /pid 2552 -f`根据pid杀死进程，解除端口占用
3. `for /r %i in (*.txt) do del %i`批量删除后缀名为txt的文件
4. `net stop mysql`关闭MySQL服务
5. `net start mysql`启动MySQL服务
6. `runas /user:administrator cmd`以管理员身份进入cmd
7. 

