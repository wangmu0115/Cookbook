### Mac系统Excel打开csv中文乱码

Excel采用的事ANSI编码，无法识别UTF-8编码下的中文，需要对文件的编码进行转换，将UTF-8转换成GBK。

```bash
iconv -f UTF-8 -t GB18030 source.csv > target.csv
```







