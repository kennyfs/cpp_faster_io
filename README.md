# c++輸入輸出壓常
搶TopCoder用，沒別的用途  
改進自[FHVirus](https://github.com/fhvirus/)的[這篇](https://pastebin.com/hxB2e6Gf)  
改變內容就只有支援負數、EOF而已
```
#include <unistd.h>
const int mxbuf=65536;//預設65536，通常改低會有更好的表現
char OB[mxbuf]; int OP;
inline char RC(){static char buf[mxbuf],*p=buf,*q=buf;return p==q&&(q=(p=buf)+read(0,buf,mxbuf))==buf?-1:*p++;}
//以下的R, W都支援負數
inline int R(){static char c;bool f=0;int a;while((c=RC())<'0'&&c!='-');if(c=='-')f=1,c=RC();a=c^'0';while((c=RC())>='0')a*=10,a+=c^'0';return f?(-a):a;}
inline void W(int n){static char buf[12],p;if(n==0)OB[OP++]='0';p=0;if(n<0)n=-n,OB[OP++]='-';while(n)buf[p++]='0'+(n%10),n/=10;for(--p;p>=0;--p)OB[OP++]=buf[p];OB[OP++]='\n';if(OP>mxbuf-20)write(1,OB,OP),OP=0;}
//可讀取以EOF結尾的輸入，回傳值-1
inline int REOF(){static char c;while((c=RC())<0&&c!=0);if(c==0)return -1;int a=c^'0';while((c=RC())>='0')a*=10,a+=c^'0';if(c==0)return -1;return a;}
```

# 壓常原理
記憶體通常都用在iostream，如果改用別的輸入輸出則可以顯著減少記憶體用量，時間通常也會跟著減少一點
