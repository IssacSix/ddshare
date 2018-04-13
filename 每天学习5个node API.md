[TOC]

## 每天学习5个node API

### path模块

####【第一天打卡 time: 04.12】basename / delimiter / dirname / extname / formate

1. path.basename()  返回path的最后一部分

   ```
   path.basename('/foo/bar/baz/asdf/quux.html');
   // 返回: 'quux.html'

   path.basename('/foo/bar/baz/asdf/quux.html', '.html');
   // 返回: 'quux'
   ```

2. path.delimiter 路径分隔属性

   ```
   process.env.PATH.split(path.delimiter)

   console.log(process.env.PATH);
   // 输出: '/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin'

   process.env.PATH.split(path.delimiter);
   // 返回: ['/usr/bin', '/bin', '/usr/sbin', '/sbin', '/usr/local/bin']
   ```

3. path.dirname()  返回路径的目录名

   ```
   path.dirname('/foo/bar/baz/asdf/index.html')
   // 返回: '/foo/bar/baz/asdf'
   ```

4. path.extname()  返回扩展名

   ```
   path.extname('index.html')
   // 返回: '.html'
   ```

5. path.formate()  返回由对象组成的一个路径字符串

   ```
   path.formate({
     dir: '',
     root: '',
     base: '',
     name: '',
     ext: ''
   })

   权重从高到低 dir => root => base => name => ext
   ```

####【第二天打卡 time: 04.13】isAbsolute / join / normalize / parse / resolve / 

1. path.isAbsolute()   返回一个路径是否是绝对路径

2. path.join()   路径进行拼接

   ```
   path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
   // 返回: '/foo/bar/baz/asdf'

   path.join('foo', {}, 'bar');
   // 抛出 'TypeError: Path must be a string. Received {}'
   ```

3. path.normalize()   路径规范化

4. path.parse()   返回path对象 与 path.formate相反

   ```
   path.parse('/home/user/dir/file.txt')
   // 返回:
   // { root: '/',
   //   dir: '/home/user/dir',
   //   base: 'file.txt',
   //   ext: '.txt',
   //   name: 'file' }
   ```

5. path.relative()   返回 from 到 to 的相对路径

   ```
   path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb');
   // 返回: '../../impl/bbb'
   ```

6. path.resolve()   返回一个绝对路径，把一个路径或者路径片段的序列解析成一个绝对路径，如果没有绝对路径则返回当前文件路径

   ```
   path.resolve('/foo/bar', './baz');
   // 返回: '/foo/bar/baz'

   path.resolve('/foo/bar', '/tmp/file/');
   // 返回: '/tmp/file'
   ```

7. path.sep()  路径片段分隔符

   ```
   'foo/bar/baz'.split(path.sep);
   // 返回: ['foo', 'bar', 'baz']
   ```

   ​