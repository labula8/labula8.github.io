cuda-helloworld

## 编译环境

C:\ProgramData\NVIDIA Corporation\CUDA Samples\v10.0

C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA

## Coding

1>D:\Program Files (x86)\Microsoft Visual Studio\2017\Community\Common7\IDE\VC\VCTargets\Microsoft.CppClean.targets(76,5): warning : 对路径“c:\users\labul_000\source\repos\hello\x64\debug\hello.exe”的访问被拒绝。
1>
1>C:\Users\labul_000\source\repos\hello>"C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\bin\nvcc.exe" -ccbin "D:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.16.27023\bin\HostX86\x64" -x cu  -I"C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\include" -I"C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0\include"  -G   --keep-dir x64\Debug -maxrregcount=0  --machine 64 --compile   -g   -DWIN32 -DWIN64 -D_DEBUG -D_CONSOLE -D_MBCS -Xcompiler "/EHsc /W3 /nologo /Od  /FS /Zi /RTC1 /MDd " -o x64\Debug\kernel.cu.obj "C:\Users\labul_000\source\repos\hello\kernel.cu" -clean
1>kernel.cu
1>Compiling CUDA source file kern

## 参考

http://www.cnblogs.com/xing901022/p/3248469.html

https://blog.csdn.net/kkk584520/article/details/9414191

https://developer.nvidia.com/cuda-downloads
https://www.nvidia.cn/object/cuda-ecosystem-cn.html