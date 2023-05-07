#### 1.   命令行运行  接受参数   执行程序

```python
from argparse import ArgumentParser

arg=ArgumentParser(description='check_url By m2')
arg.add_argument("-u","--url",required=True, help="Target URL; Example:http://ip:port")
args=arg.parse_args()
url=args.url
```

