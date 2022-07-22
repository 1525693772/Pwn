## 关闭alarm
```
sed -i s/alarm/isnan/g  ./ELF_Name
sed -i s/sleep/isnan/g  ./wdb_2018_1st_babyheap
关闭alarm和sleep，便于调试
```

## Ubuntu Libc版本

```
Ubuntu20.04：libc-2.31
Ubuntu18.04：linc-2.27
Ubuntu16.04：libc-2.23
Ubuntu14.04：libc-2.19
```


## 更换Libc挂载elf
```
p = process(['./bin'],env={"LD_PRELOAD":"./libc-2.23.so"})
```

## PwnGdb
```
开启PIE时，断点设置在偏移后的0xABCD处:
	b *$rebase(0xABCD)
```

## Exp
```
pause()
	停在该处，生成一个pid号，可以重开一个终端打开Gdb并且attach这个pid号继续调试
```

## objdump查看glibc中函数的偏移量
```
objdump /lib32/libc.so.6 -D -M intel | grep __malloc_hook
```



## 更改elf文件的ld和libc

```
#生成所需的符号链接
ln -s /home/pwn/desktop/Libc/glibc-all-in-one/libs/2.23-0ubuntu11.3_amd64/libc-2.23.so ./23_11-linux.so.2
 #./23_11-linux.so.2是自己起的名。23代表glibc版本,11代表ubuntu后面的数字(单纯为了好记)

patchelf --set-interpreter /lib64/23_11_64-linux.so.2 ./bin
patchelf --replace-needed libc.so.6 /home/pwn/desktop/Libc/glibc-all-in-one/libs/2.23-0ubuntu11.3_amd64/libc-2.23.so ./chunk_extend_2
#libc.so.6为需要替换的libc路径 第二个参数是需要加载的glibc的目录    
#bin 是二进制文件
$ ldd ./bin #查看elf的ld和libc
```



## Shellcode

```
shellcode=asm(shellcraft.sh())
shellcodeasm('pop eax;pop ebx')
```



# close(1&0)关闭标准输出

```
get shell 后执行 ‘exec 1>&0’ 重定向输出
```



# SSh

```
s = ssh(host='node4.buuoj.cn',port=29486,
         user='unlink',password='guest')
a = s.process("./unlink") 
```



# Ascii ShellCode

```
64:
Ph0666TY1131Xh333311k13XjiV11Hc1ZXYf1TqIHf9kDqW02DqX0D1Hu3M2G0Z2o4H0u0P160Z0g7O0Z0C100y5O3G020B2n060N4q0n2t0B0001010H3S2y0Y0O0n0z01340d2F4y8P115l1n0J0h0a070t
```





## ciscn_2019_n_3？？？？

