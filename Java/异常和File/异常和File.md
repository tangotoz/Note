# 异常和File

## File

**绝对路径**：从文件系统的根目录开始，唯一标识文件或目录的位置

**相对路径**：相对于当前工作目录表示文件或目录的位置

- File对象就表示一个路径，可以是文件的路径，也可以是文件夹的路径
- 这个路径可以是存在的，也允许是不存在的

| 方法名称                                 | 说明                                           |
| ---------------------------------------- | ---------------------------------------------- |
| public File(String pathName)             | 根据文件路径创建文件对象                       |
| public File(String parent, String child) | 根据父路径名字符串和子路径名字符串创建文件对象 |
| public File(File parent, String child)   | 根据父路径相应的文件和子路径字符串创建对象     |

### File的常见成员方法

判断、获取相关的方法

| 方法名称                        | 说明                             |
| ------------------------------- | -------------------------------- |
| public boolean isDirectory()    | 判断此路径表示的File是否为文件夹 |
| public boolean isFile()         | 判断此路径名表示的File是否为文件 |
| public boolean exists()         | 判断此路径名表示的File是否存在   |
| public long length()            | 返回文件的大小（字节数量）       |
| public String getAbsolutePath() | 返回文件的绝对路径               |
| public String getPath()         | 返回定义文件时所使用的路径       |
| public String getName()         | 返回文件的名称，带后缀           |
| public long lastModified()      | 返回文件的最后修改时间           |

创建、删除相关的方法

| 方法名称                       | 说明                 |
| ------------------------------ | -------------------- |
| public boolean createNewFile() | 创建一个新的空的文件 |
| public boolean mkdir()         | 创建单级文件夹       |
| public boolean mkdirs()        | 创建多级文件夹       |
| public boolean delete()        | 删除文件、空文件夹   |

