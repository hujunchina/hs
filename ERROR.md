![image-20210218194434000](C:/Users/Administrator/AppData/Roaming/Typora/typora-user-images/image-20210218194434000.png)

枚举类型定义冲突：

就是rk库里面已经定义了PIXEL_FORMAT_BUTT，在rkmedia_venc.h中；

而又在isp_comm.h中重复定义了这个：

改成PIXEL_FORMAT_BUTT_888就行了

这是编程书写不注意导致的，他还改了很多，都以888结尾的。