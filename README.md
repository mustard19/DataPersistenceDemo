# DataPersistenceDemo
# iOS数据持久化（记录）

## 1.plist文件
即属性列表文件，全名是Property List，这种文件的扩展名为.plist，因此，通常被叫做plist文件。它是一种用来存储串行化后的对象的文件，用于存储程序中经常用到且数据量小而不经常改动的数据。

可以存储的类型:NSNumber，NSString，NSDate，NSData ,NSArray，NSDictionary，BOOL.

不支持自定义对象的存储.

plist的创建方式有两种:command + n 创建和纯代码创建,不同的创建方式使用方法也自然不同。

command + n 创建:
````
    读取:
    NSString *plistPath = [[NSBundle mainBundle]pathForResource:@"myTest" ofType:@"plist"];
    NSMutableDictionary *dataDic = [NSMutableDictionary dictionaryWithContentsOfFile:plistPath];
    //    NSMutableArray *dataArray = [NSMutableArray arrayWithContentsOfFile:plistPath];
    NSLog(@"%@",dataDic);
    
    修改:
    [dataDic setObject:@"男" forKey:@"sex"];
    [dataDic setObject:@15 forKey:@"age"];
    [dataDic writeToFile:plistPath atomically:YES];
    NSLog(@"----%@",dataDic);
````

纯代码创建:
````
    创建:
    NSArray *sandBoxPath = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsPath = [sandBoxPath objectAtIndex:0];
    NSString *plistPath = [documentsPath stringByAppendingPathComponent:@"myTestPlist.plist"];
    NSLog(@"%@",plistPath);

    写入:
    NSMutableDictionary *dic = [NSMutableDictionary dictionary];
    [dic setObject:@"18" forKey:@"age"];
    [dic setObject:@"胡杨" forKey:@"name"];
    [dic writeToFile:plistPath atomically:YES];

    读取:
    NSArray *sandBoxPath = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    NSString *documentsPath = [sandBoxPath objectAtIndex:0];
    NSString *plistPath = [documentsPath stringByAppendingPathComponent:@"myTestPlist.plist"];
    NSLog(@"%@",plistPath);

    NSMutableDictionary *dataDic = [NSMutableDictionary dictionaryWithContentsOfFile:plistPath];
    NSLog(@"-----%@",dataDic);

    修改:
    与command+n方法相同.
````

需要注意的问题：如果需要存储自定义类型的数据需要先进行序列化。




##
##
##
## 2.NSUserDefaults
用于存储用户的偏好设置、用户信息（如用户名、是否自动登录、字体大小等）。

数据自动保存在沙盒的Libarary/Preferences 目录下。

NSUserDefaults将输入的数据储存在.plist格式的文件下，这种存储方式就决定了它的安全性几乎为0，所以不建议存储一些敏感信息如:用户密码、token、加密私钥等。

它能存储的数据类型为：NSNumber（NSInteger、float、double、BOOL），NSString，NSDate，NSArray，NSDictionary，NSData。

不支持自定义对象的存储.

需要注意的问题:
1.NSUserDefaults存储的数据都是不可变的，想将可变数据存入需要先转为不可变才可以存储。

2.NSUserDefaults是定时把缓存中的数据写入磁盘的，而不是即时写入，为了防止在写完NSUserDefaults后程序退出导致的数据丢失，可以在写入数据后使用synchronize强制立即将数据写入磁盘。

````
// code block: test code
NSUserDefaults *userDefault = [NSUserDefaults standardUserDefaults];
[userDefault setInteger:1 forKey:@"integer"];
[userDefault setBool:YES forKey:@"BOOL"];
[userDefault setFloat:6.5 forKey:@"float"];
[userDefault setObject:@"123" forKey:@"numberString"];
NSString *numberString = [userDefault objectForKey:@"numberString"];
BOOL myBool = [userDefault boolForKey:@"BOOl"];
[userDefault removeObjectForKey:@"float"];
[userDefault synchronize];
````


##
##
##
## 3.钥匙串（keychain）





## 4.归档





## 5.沙盒





## 6.数据库（sqllite）





## 7.CoreData


