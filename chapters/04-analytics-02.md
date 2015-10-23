#Github项目分析二

    
让我们分析之前的程序，然后再想办法做出优化。网上看到一篇文章[http://www.huyng.com/posts/python-performance-analysis/](http://www.huyng.com/posts/python-performance-analysis/)讲的就是分析这部分内容的。
    
##Time Python分析

分析程序的运行时间
     
```bash     
$time python handle.py
```

结果便是，但是对于我们的分析没有一点意义

```
    real	0m43.411s
    user	0m39.226s
    sys	0m0.618s
```

##line_profiler python

```bash
sudo ARCHFLAGS="-Wno-error=unused-command-line-argument-hard-error-in-future" easy_install line_profiler
```

然后在我们的``parse_data.py``的``handle_json``前面加上``@profile``

```python
@profile
def handle_json(jsonfile):
    f = open(jsonfile, "r")
    dataarray = []
    datacount = 0

    for line in open(jsonfile):
        line = f.readline()
        lin = json.loads(line)
        date = dateutil.parser.parse(lin["created_at"])
        datacount += 1
        dataarray.append(date.minute)

    f.close()
    return datacount, dataarray
```

Line_profiler带了一个分析脚本``kernprof.py``，so

```bash
kernprof.py -l -v handle.py
```

我们便会得到下面的结果

```
Wrote profile results to handle.py.lprof
Timer unit: 1e-06 s

File: parse_data.py
Function: handle_json at line 15
Total time: 127.332 s

Line #      Hits         Time  Per Hit   % Time  Line Contents
==============================================================
    15                                           @profile
    16                                           def handle_json(jsonfile):
    17        19          636     33.5      0.0      f = open(jsonfile, "r")
    18        19           21      1.1      0.0      dataarray = []
    19        19           16      0.8      0.0      datacount = 0
    20
    21    212373       730344      3.4      0.6      for line in open(jsonfile):
    22    212354      2826826     13.3      2.2          line = f.readline()
    23    212354     13848171     65.2     10.9          lin = json.loads(line)
    24    212354    109427317    515.3     85.9          date = dateutil.parser.parse(lin["created_at"])
    25    212354       238112      1.1      0.2          datacount += 1
    26    212354       260227      1.2      0.2          dataarray.append(date.minute)
    27
    28        19          349     18.4      0.0      f.close()
    29        19           20      1.1      0.0      return datacount, dataarray
```

于是我们就发现我们的瓶颈就是从读取``created_at``，即创建时间。。。以及解析json，反而不是我们关心的IO，果然``readline``很强大。

##memory_profiler

首先我们需要install memory_profiler:

```bash
$ pip install -U memory_profiler
$ pip install psutil
```

如上，我们只需要在``handle_json``前面加上``@profile``

```bash
python -m memory_profiler handle.py
```

于是

```
Filename: parse_data.py
    
Line #    Mem usage    Increment   Line Contents
================================================
    13   39.930 MiB    0.000 MiB   @profile
    14                             def handle_json(jsonfile):
    15   39.930 MiB    0.000 MiB       f = open(jsonfile, "r")
    16   39.930 MiB    0.000 MiB       dataarray = []
    17   39.930 MiB    0.000 MiB       datacount = 0
    18
    19   40.055 MiB    0.125 MiB       for line in open(jsonfile):
    20   40.055 MiB    0.000 MiB           line = f.readline()
    21   40.066 MiB    0.012 MiB           lin = json.loads(line)
    22   40.055 MiB   -0.012 MiB           date = dateutil.parser.parse(lin["created_at"])
    23   40.055 MiB    0.000 MiB           datacount += 1
    24   40.055 MiB    0.000 MiB           dataarray.append(date.minute)
    25
    26                                 f.close()
    27                                 return datacount, dataarray
```

##objgraph python

安装objgraph

```bash
pip install objgraph
```

我们需要调用他

```python
import pdb;
```

以及在需要调度的地方加上

```python
pdb.set_trace()
```

接着会进入``command``模式

```python
(pdb) import objgraph
(pdb) objgraph.show_most_common_types()
```

然后我们可以找到。。

```
function                   8259
dict                       2137
tuple                      1949
wrapper_descriptor         1625
list                       1586
weakref                    1145
builtin_function_or_method 1117
method_descriptor          948
getset_descriptor          708
type                       705
```

也可以用他生成图形，貌似这里是用``dot``生成的，加上``python-xdot``

很明显的我们需要一个数据库。

如果我们每次都要花同样的时间去做一件事，去扫那些数据的话，那么这是最好的打发时间的方法。

##python SQLite3 查询数据

我们创建了一个名为``userdata.db``的数据库文件，然后创建了一个表，里面有owner,language,eventtype,name url

```python
def init_db():
    conn = sqlite3.connect('userdata.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE userinfo (owner text, language text, eventtype text, name text, url text)''')
```

接着我们就可以查询数据，这里从结果讲起。

```python
def get_count(username):
    count = 0
    userinfo = []
    condition = 'select * from userinfo where owener = \'' + str(username) + '\''
    for zero in c.execute(condition):
        count += 1
        userinfo.append(zero)

    return count, userinfo
```

当我查询``gmszone``的时候，也就是我自己就会有如下的结果

```bash
(u'gmszone', u'ForkEvent', u'RESUME', u'TeX', u'https://github.com/gmszone/RESUME')
(u'gmszone', u'WatchEvent', u'iot-dashboard', u'JavaScript', u'https://github.com/gmszone/iot-dashboard')
(u'gmszone', u'PushEvent', u'wechat-wordpress', u'Ruby', u'https://github.com/gmszone/wechat-wordpress')
(u'gmszone', u'WatchEvent', u'iot', u'JavaScript', u'https://github.com/gmszone/iot')
(u'gmszone', u'CreateEvent', u'iot-doc', u'None', u'https://github.com/gmszone/iot-doc')
(u'gmszone', u'CreateEvent', u'iot-doc', u'None', u'https://github.com/gmszone/iot-doc')
(u'gmszone', u'PushEvent', u'iot-doc', u'TeX', u'https://github.com/gmszone/iot-doc')
(u'gmszone', u'PushEvent', u'iot-doc', u'TeX', u'https://github.com/gmszone/iot-doc')
(u'gmszone', u'PushEvent', u'iot-doc', u'TeX', u'https://github.com/gmszone/iot-doc')
109
````

一共有109个事件，有``Watch``,``Create``,``Push``,``Fork``还有其他的，
项目主要有``iot``,``RESUME``,``iot-dashboard``,``wechat-wordpress``,
接着就是语言了，``Tex``,``Javascript``,``Ruby``,接着就是项目的url了。

值得注意的是。

```bash
-rw-r--r--   1 fdhuang staff 905M Apr 12 14:59 userdata.db
```

这个数据库文件有**905M**，不过查询结果相当让人满意，至少相对于原来的结果来说。

Python自带了对SQLite3的支持，然而我们还需要安装SQLite3

```bash
brew install sqlite3
```

或者是

```bash   
sudo port install sqlite3
```

或者是Ubuntu的

```bash
sudo apt-get install sqlite3
```

openSUSE自然就是

```bash
sudo zypper install sqlite3
```

不过，用yast2也很不错，不是么。。

###数据导入

需要注意的是这里是需要python2.7，起源于对gzip的上下文管理器的支持问题

```python
def handle_gzip_file(filename):
    userinfo = []
    with gzip.GzipFile(filename) as f:
        events = [line.decode("utf-8", errors="ignore") for line in f]

        for n, line in enumerate(events):
            try:
                event = json.loads(line)
            except:

                continue

            actor = event["actor"]
            attrs = event.get("actor_attributes", {})
            if actor is None or attrs.get("type") != "User":
                continue

            key = actor.lower()

            repo = event.get("repository", {})
            info = str(repo.get("owner")), str(repo.get("language")), str(event["type"]), str(repo.get("name")), str(
                repo.get("url"))
            userinfo.append(info)

    return userinfo

def build_db_with_gzip():
    init_db()
    conn = sqlite3.connect('userdata.db')
    c = conn.cursor()

    year = 2014
    month = 3

    for day in range(1,31):
        date_re = re.compile(r"([0-9]{4})-([0-9]{2})-([0-9]{2})-([0-9]+)\.json.gz")

        fn_template = os.path.join("march",
                                   "{year}-{month:02d}-{day:02d}-{n}.json.gz")
        kwargs = {"year": year, "month": month, "day": day, "n": "*"}
        filenames = glob.glob(fn_template.format(**kwargs))

        for filename in filenames:
            c.executemany('INSERT INTO userinfo VALUES (?,?,?,?,?)', handle_gzip_file(filename))

    conn.commit()
    c.close()
```

``executemany``可以插入多条数据，对于我们的数据来说，一小时的文件大概有五六千个会符合我们上面的安装，也就是有``actor``又有``type``才是我们需要记录的数据，我们只需要统计用户的那些事件，而非全部的事件。

我们需要去遍历文件，然后找到合适的部分，这里只是要找``2014-03-01``到``2014-03-31``的全部事件，而光这些数据的gz文件就有1.26G，同上面那些解压为json文件显得不合适，只能用遍历来处理。

这里参考了osrc项目中的写法，或者说直接复制过来。

首先是正规匹配

```python
date_re = re.compile(r"([0-9]{4})-([0-9]{2})-([0-9]{2})-([0-9]+)\.json.gz")
```

不过主要的还是在于``glob.glob``

> glob是python自己带的一个文件操作相关模块，用它可以查找符合自己目的的文件，就类似于Windows下的文件搜索，支持通配符操作。

这里也就用上了``gzip.GzipFile``又一个不错的东西。

最后代码可以见

[github.com/gmszone/ml](http://github.com/gmszone/ml)

更好的方案？

##Redis

查询用户事件总数

```python
import redis
r = redis.StrictRedis(host='localhost', port=6379, db=0)
pipe = pipe = r.pipeline()
pipe.zscore('osrc:user',"gmszone")
pipe.execute()
```

系统返回了``227.0``,试试别人。

```bash
>>> pipe.zscore('osrc:user',"dfm")
<redis.client.StrictPipeline object at 0x104fa7f50>
>>> pipe.execute()
[425.0]
>>>
```

看看主要是在哪一天提交的

```python
>>> pipe.hgetall('osrc:user:gmszone:day')
<redis.client.StrictPipeline object at 0x104fa7f50>
>>> pipe.execute()
[{'1': '51', '0': '41', '3': '17', '2': '34', '5': '28', '4': '22', '6': '34'}]
```

结果大致如下图所示:

![SMTWTFS](./img/smtwtfs.png)

看看主要的事件是？

    >>> pipe.zrevrange("osrc:user:gmszone:event".format("gmszone"), 0, -1,withscores=True)
    <redis.client.StrictPipeline object at 0x104fa7f50>
    >>> pipe.execute()
    [[('PushEvent', 154.0), ('CreateEvent', 41.0), ('WatchEvent', 18.0), ('GollumEvent', 8.0), ('MemberEvent', 3.0), ('ForkEvent', 2.0), ('ReleaseEvent', 1.0)]]
    >>>

![Main Event](./img/main-events.png)

蓝色的就是push事件，黄色的是create等等。

到这里我们算是知道了OSRC的数据库部分是如何工作的。

###Redis 查询

主要代码如下所示

```python
def get_vector(user, pipe=None):

    r = redis.StrictRedis(host='localhost', port=6379, db=0)
    no_pipe = False
    if pipe is None:
        pipe = pipe = r.pipeline()
        no_pipe = True

    user = user.lower()
    pipe.zscore(get_format("user"), user)
    pipe.hgetall(get_format("user:{0}:day".format(user)))
    pipe.zrevrange(get_format("user:{0}:event".format(user)), 0, -1,
                   withscores=True)
    pipe.zcard(get_format("user:{0}:contribution".format(user)))
    pipe.zcard(get_format("user:{0}:connection".format(user)))
    pipe.zcard(get_format("user:{0}:repo".format(user)))
    pipe.zcard(get_format("user:{0}:lang".format(user)))
    pipe.zrevrange(get_format("user:{0}:lang".format(user)), 0, -1,
                   withscores=True)

    if no_pipe:
        return pipe.execute()
```

结果在上一篇中显示出来了，也就是

```
[227.0, {'1': '51', '0': '41', '3': '17', '2': '34', '5': '28', '4': '22', '6': '34'}, [('PushEvent', 154.0), ('CreateEvent', 41.0), ('WatchEvent', 18.0), ('GollumEvent', 8.0), ('MemberEvent', 3.0), ('ForkEvent', 2.0), ('ReleaseEvent', 1.0)], 0, 0, 0, 11, [('CSS', 74.0), ('JavaScript', 60.0), ('Ruby', 12.0), ('TeX', 6.0), ('Python', 6.0), ('Java', 5.0), ('C++', 5.0), ('Assembly', 5.0), ('C', 3.0), ('Emacs Lisp', 2.0), ('Arduino', 2.0)]]
```

有意思的是在这里生成了和自己相近的人

```
['alesdokshanin', 'hjiawei', 'andrewreedy', 'christj6', '1995eaton']
```

osrc最有意思的一部分莫过于flann，当然说的也是系统后台的设计的一个很关键及有意思的部分。

##邻近算法

邻近算法是在这个分析过程中一个很有意思的东西。

>邻近算法，或者说K最近邻(kNN，k-NearestNeighbor)分类算法可以说是整个数据挖掘分类技术中最简单的方法了。所谓K最近邻，就是k个最近的邻居的意思，说的是每个样本都可以用她最接近的k个邻居来代表。

换句话说，我们需要一些样本来当作我们的分析资料，这里东西用到的就是我们之前的。

```
[227.0, {'1': '51', '0': '41', '3': '17', '2': '34', '5': '28', '4': '22', '6': '34'}, [('PushEvent', 154.0), ('CreateEvent', 41.0), ('WatchEvent', 18.0), ('GollumEvent', 8.0), ('MemberEvent', 3.0), ('ForkEvent', 2.0), ('ReleaseEvent', 1.0)], 0, 0, 0, 11, [('CSS', 74.0), ('JavaScript', 60.0), ('Ruby', 12.0), ('TeX', 6.0), ('Python', 6.0), ('Java', 5.0), ('C++', 5.0), ('Assembly', 5.0), ('C', 3.0), ('Emacs Lisp', 2.0), ('Arduino', 2.0)]]
```

在代码中是构建了一个points.h5的文件来分析每个用户的points，之后再记录到hdf5文件中。

```
[ 0.00438596  0.18061674  0.2246696   0.14977974  0.07488987  0.0969163
    0.12334802  0.14977974  0.          0.18061674  0.          0.          0.
    0.00881057  0.          0.          0.03524229  0.          0.
    0.01321586  0.          0.          0.          0.6784141   0.
    0.07929515  0.00440529  1.          1.          1.          0.08333333
    0.26431718  0.02202643  0.05286344  0.02643172  0.          0.01321586
    0.02202643  0.          0.          0.          0.          0.          0.
    0.          0.          0.00881057  0.          0.          0.          0.
    0.          0.          0.          0.          0.          0.          0.
    0.          0.          0.          0.          0.00881057]
```

这里分析到用户的大部分行为，再找到与其行为相近的用户，主要的行为有下面这些:

 - 每星期的情况
 - 事件的类型
 - 贡献的数量，连接以及语言
 - 最多的语言

osrc中用于解析的代码

```python
def parse_vector(results):
    points = np.zeros(nvector)
    total = int(results[0])

    points[0] = 1.0 / (total + 1)

    # Week means.
    for k, v in results[1].iteritems():
        points[1 + int(k)] = float(v) / total

    # Event types.
    n = 8
    for k, v in results[2]:
        points[n + evttypes.index(k)] = float(v) / total

    # Number of contributions, connections and languages.
    n += nevts
    points[n] = 1.0 / (float(results[3]) + 1)
    points[n + 1] = 1.0 / (float(results[4]) + 1)
    points[n + 2] = 1.0 / (float(results[5]) + 1)
    points[n + 3] = 1.0 / (float(results[6]) + 1)

    # Top languages.
    n += 4
    for k, v in results[7]:
        if k in langs:
            points[n + langs.index(k)] = float(v) / total
        else:
            # Unknown language.
            points[-1] = float(v) / total

    return points
```

这样也就返回我们需要的点数，然后我们可以用``get_points``来获取这些

```python
def get_points(usernames):
    r = redis.StrictRedis(host='localhost', port=6379, db=0)
    pipe = r.pipeline()

    results = get_vector(usernames)
    points = np.zeros([len(usernames), nvector])
    points = parse_vector(results)
    return points
```

就会得到我们的相应的数据，接着找找和自己邻近的，看看结果。

```
[ 0.01298701  0.19736842  0.          0.30263158  0.21052632  0.19736842
    0.          0.09210526  0.          0.22368421  0.01315789  0.          0.
    0.          0.          0.          0.01315789  0.          0.
    0.01315789  0.          0.          0.          0.73684211  0.          0.
    0.          1.          1.          1.          0.2         0.42105263
    0.09210526  0.          0.          0.          0.          0.23684211
    0.          0.          0.03947368  0.          0.          0.          0.
    0.          0.          0.          0.          0.          0.          0.
    0.          0.          0.          0.          0.          0.          0.
    0.          0.          0.          0.        ]
```

真看不出来两者有什么相似的地方 。。。。  
