# 瞎折腾环境踩坑记录

## ubuntu 22 (Orbstack) 安装 vivado
如果安装界面卡在 Generating installed device list
```
sudo ln -s /lib/x86_64-linux-gnu/libtinfo.so.6 /lib/x86_64-linux-gnu/libtinfo.so.5
```

## 在 orbstack 使用 vivado
### CLI
在终端中使用 vivado 可能需要在 vivado 前加上 LD_PRELOAD 参数
```
PRELOAD_LIB = /lib/x86_64-linux-gnu/libudev.so.1:/lib/x86_64-linux-gnu/libselinux.so.1
LD_PRELOAD=$(PRELOAD_LIB) $(vivado) -mode batch -source xxx.tcl
```

### GUI （未验证）
假设启动器默认命令为 
```
/home/xxx/tools/Xilinx//Vivado/2022.2/bin/vivado
```

新建 start_vivado.sh 输入
```
#!/bin/bash
LD_PRELOAD=/lib/x86_64-linux-gnu/libudev.so.1:/lib/x86_64-linux-gnu/libselinux.so.1 /home/xxx/tools/Xilinx//Vivado/2022.2/bin/vivado  "$@"
```

将启动器默认命令改为
```
/home/xxx/tools/Xilinx//Vivado/2022.2/bin/start_vivado.sh
```
