# 「Draw With Python」使用多进程绘制

## 装模作样的引言

2%|█         ：（          | 16/907 [01:16<1:07:58, 4.58s/it]



## 问题的提出

我喜欢使用matplotlib画图，但它在处理大幅图像的时候慢吞吞的动作快要消磨殆尽我对它的喜爱。

~~宁配吗~~

问题重现：现在我需要把一幅图片的局部展示出来，涉及大矩阵（张量）操作，可能是延误时间的根源。可是目前我对matplotlib的底层完全不了解，所以无从判断和优化。时间不够，进程来凑，我决定使用multiprocess库试一试多进程画图。

## 问题的解决尝试：multiprocessing

Python [multiprocessing](https://docs.python.org/2/library/multiprocessing.html) 库实现并行操作（多CPU)





blah-blah：之前总是把类似的问题和解决思路写在[typora](https://typora.io/)里，用github和github.io查看，但终究还是繁琐；想要自己建站，但最近查得严（整个服务器光host几个http太浪费了）；简书初来乍到，~~不支持markdown有些失落~~，但颜值正义，CSDN广告太多且印象不好，cnblog密码忘了不想再申请，希望我能在现在的路上坚持得更久一些。*错怪简书了，默认富文本编辑器罢了，而且不实时渲染（这样的话就没人帮我打列表的空格和横线了）聪明的人应该在typora 上编辑好再贴过来。*



## 新的问题：

  2%|██                                                                  | 18/907 [01:54<1:33:59,  6.34s/it]

Maximum number of clients reachedqt.qpa.screen: QXcbConnection: Could not connect to display :0
Could not connect to any X display.