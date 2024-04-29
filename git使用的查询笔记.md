# 1.git没有清理干净

备注：下面命令在windows界面是在git bash运行的，要先进入本地clone的文件夹下。

在 Windows 10 上使用 Git 进行 push 操作时出现 "Git没有清理干净" 的错误可能是由于一些临时文件或旧版本文件未被清理导致的。这个问题通常可以通过以下方法来解决：

1. **清理未跟踪的文件**： 在 Git 仓库根目录下执行以下命令，清理掉未跟踪的文件：

   ```shell
   git clean -df
   ```

2. **重置修改的文件**： 如果上述命令没有解决问题，可以尝试重置所有修改的文件：

   ```shell
   git reset --hard
   ```

3. **清理 Git 的临时文件**： 有时 Git 的一些临时文件可能会导致问题，可以手动清理它们：

   ```shell
   rm -rf .git/index.lock
   ```

4. **检查文件权限**： 确保你有权限对 Git 仓库进行操作。

5. **尝试重新克隆仓库**： 如果以上方法都没有解决问题，可以尝试删除本地仓库并重新克隆一份。

在执行以上操作前，请确保你理解它们的影响，并且备份你的重要数据，以免造成不可逆的损失。



这些操作会产生以下影响：

1. **清理未跟踪的文件 (`git clean -df`)：**
   - 会删除仓库中未被 Git 跟踪的文件和文件夹，包括你可能不需要的临时文件或编译生成的文件。
   - 慎重使用，确保你不需要这些文件，因为它们将被永久删除。
2. **重置修改的文件 (`git reset --hard`)：**
   - 会将所有已修改但未提交的文件恢复到它们在最后一次提交时的状态，即取消所有的本地修改。
   - 这将清除你在本地对文件的所有更改，所以在执行之前请确保你不需要这些更改。
3. **清理 Git 的临时文件 (`rm -rf .git/index.lock`)：**
   - 删除 Git 锁文件，这些锁文件通常在 Git 操作被异常中断时留下，阻止其他 Git 操作。
   - 这个命令是针对特定问题的，如果你遇到了 Git 操作被锁定的情况，可以尝试清理这些锁文件。
4. **检查文件权限：**
   - 确保你有足够的权限对 Git 仓库及其文件进行操作，避免出现权限相关的错误。
5. **重新克隆仓库：**
   - 如果其他方法无效，你可以尝试删除本地仓库并重新克隆一份。这将重置仓库到最初的状态，但同时也会丢失你本地的所有更改。

这些操作都会对你的 Git 仓库产生不同程度的影响，请在执行之前确保理解其作用，并且备份重要数据以防止不可逆的损失。



要检查文件权限，可以使用 `ls -l` 命令查看文件的详细列表，其中包括文件权限信息。在这个列表中，文件权限会显示在每个文件条目的开头部分。例如：

```shell
ls -l
```

这将列出当前目录下所有文件的详细信息，包括文件权限、所有者、文件大小等等。权限部分的形式通常如下所示：

```shell
-rw-r--r--  1 user group  4096 Apr 27 08:00 example.txt
```

其中，第一列 `-rw-r--r--` 表示文件的权限。在这个例子中，第一个字符是文件类型（`-` 表示普通文件），接下来的三组字符（每组三个字符）分别表示文件所有者的权限、文件所属组的权限和其他用户的权限。

每个权限组都由三个字符组成，表示读取（`r`）、写入（`w`）和执行（`x`）权限。如果有权限，相应的字符将显示，如果没有，则显示 `-`。

例如，`-rw-r--r--` 表示：

- 文件所有者具有读写权限，但没有执行权限。
- 文件所属组具有读取权限，但没有写入和执行权限。
- 其他用户具有读取权限，但没有写入和执行权限。

通过查看这些权限信息，你可以了解文件谁拥有何种权限，以及是否有足够的权限来执行所需的操作。



# 2.git介绍、下载和使用

git就是一个免费开源的分布式版本控制系统。

版本控制就是管理代码。

分布式用来区分于集中式，集中式只有一个档案馆，分布式有多个档案馆，可以在自己的档案馆处理自己的版本，自己的版本做好了，就可以拿过去和别人的版本进行合并。

下载地址：https://git-scm.com/download

```shell
# 配置名字和邮箱：
git config --global user.name "laowang"
git config --global user.email laowang@example.com
```

```shell
# 创建仓库：（在文件夹中使用）
git init
```

```shell
# 克隆
git clone url
```

创建完仓库后，会赋予这个仓库中每一个文件一个状态；如果是自己新建的仓库的话，那么仓库里面所有的文件都是未被跟踪的。当生成一个版本之后，这个未被跟踪的文件就不会在这个版本里，那么它之前的状态或者它之前哪里修改那就都无从谈起了，现在可以单独的跟踪一个文件或者跟踪一个目录。

```shell
# 跟踪一个文件或者一个目录
git add <name>
```

如果一个目录或者文件被跟踪，那么这辈子在这个仓库里都是被跟踪的。如果想让它不被跟踪的话，可以通过git rm <name>删掉或者git rm --cache <name>。

```shell
# 想让被跟踪的文件或目录不被跟踪（删掉文件）
git rm <name>	
```

```shell
# 想让被跟踪的文件或目录不被跟踪（保留文件，但是不被跟踪）
git rm --cache <name>	
```

```shell
# 对跟踪的文件进行修改，修改完成之后把跟踪的文件的状态设置为缓存（暂存）状态
git add <file-name>
```

```shell
# 不想设置为缓存状态 或者 取消缓存状态
git reset HEAD <name>
```

```shell
# 提交此次修改
git commit
git commit -m 'laotie666'	# 'laotie666'是本次提交文件的备注，备注此次提交修改了什么
```

一个文件的四个状态：

未跟踪：新建一个仓库，这个仓库里都是未跟踪状态的文件。

未修改：

已修改：

暂存：

除了未跟踪就是跟踪了。

![image-20240427231124592](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240427231124592.png)

对暂存的文件进行commit操作，最终实现一个新的版本。

```shell
# 取消上次的提交(但是不能撤销第1次的提交)
git reset head~ --soft
```

```shell
# 查看文件的状态
git status
```

git commit之后的git status是没有修改也没有提交。

```shell
# 查看哪里被修改了
git diff
```

```shell
# 查看提交的历史
git log
# 出来的记过：commit后面的乱码是提交的一个哈希值，是唯一的，可以通过哈希值找到本次的提交，还有提交作者和提交时间，还有提交的备注信息

# 美化输出
git log --pretty=oneline	# 把每次提交的信息变为一行
git log --pretty=format:"%h-%m,%ar:%s"	# 自定义一个格式
# 常用的格式信息：%h：简化哈希 %an：作者名字 %ar：修订日期（距离今天） %ad：修订日期 %s：提交说明
```

```shell
# 查看命令
git -h
```

远程仓库的创建和使用：

创建：

1.右上角点击+号，点击New repository；

![image-20240428024001156](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428024001156.png)

2.进去之后输入仓库名字，然后选择public/private，然后点击create repository。（这样做就创建了一个空项目（仓库））

![image-20240428024427383](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428024427383.png)

3.然后会显示一个下面的界面，下面的https就是clone的时候的地址。

![image-20240428024757919](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428024757919.png)



使用：

1.复制好远程仓库的链接，然后右击空白桌面进入git bash，进入本地的项目文件夹。

```shell
git remote add 远程仓库的名字（一般叫origin） 远程仓库的链接（就是https）	# 添加或者链接远程仓库
git remote	# 列出所有远程主机/查看所有仓库
git remote rename 原先的仓库名字 修改之后的名字	# 修改远程仓库的名字
```

```shell
git push 远程仓库的名字（origin） master（分支） # 将本地的master分支代码推送到远程的仓库
# 之后会要输入用户名和密码，第一次会错误，告诉github不支持用户名和密码的这个认证方式了。
```

2.创建令牌。（解决上面用户名和密码的哪个错误）

需要先回到github页面，在右上角点击用户头像，然后点击setting；

![image-20240428030158249](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428030158249.png)

点击setting之后，拉倒最下面点击Developer settings;

![image-20240428030332813](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428030332813.png)

点击Developer settings之后，点击Personal access tokens中的Tokens（classic）；



![image-20240428030513777](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428030513777.png)

点击Tokens（classic）之后，然后点击Generate new token中的Generate new token (classic)；（就是现在需要创建一个令牌，然后拿这个令牌去当密码，然后生成一个普通的(金典的)。）

![image-20240428030836219](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428030836219.png)

点击进来之后填写Note，就是自己用来干嘛的，不写也可以，选择多少天，一般默认30天，然后勾选repo把有关仓库的权限打开。

![image-20240428033725585](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428033725585.png)

然后点击Generate token进行生成。

![image-20240428034018096](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428034018096.png)

点击之后会出现这个界面：

![image-20240428034403202](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428034403202.png)



3.现在在password的地方使用上面复制的token。

```shell
git remote add 远程仓库的名字（一般叫origin） 远程仓库的链接（就是https）	# 添加或者链接远程仓库
# 然后输入用户名，在输入密码的地方输入上面复制的token，然后就可以上传成功了。
```

会是一个类似下面的界面，表示上传成功（将本地的master分支代码推送到远程的仓库）了：

![image-20240428035201897](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428035201897.png)

4.用生成token的方式鉴权优点麻烦，下面还有一个比较简单的方式，就是通过ssh协议去鉴权。

```shell
cd ~/.ssh	# 进入到用户的ssh目录里面
ssh-keygen -t rsa -b 4096 -C "1982782238@qq.com" #生成一个ssh秘钥，-t选择一个生成的算法，rsa是选择的算法，-b可以选择大小，-C可以添加评论，这个评论随便写，github推荐写的是个人的邮箱
# 回车后会让起秘钥的名字，这里随便，比如写test就可以
# 接下来会让输入密码
# 然后会生成一个秘钥，可以使用ls查看，以上面秘钥的名字test举例，会有一个test的私钥和test.pub的公钥
#然后可以cat test.pub进行查看公钥，然后复制查看的内容
```

然后点击github的setting；

![image-20240428040540014](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428040540014.png)

然后选择SSH and GPG keys，点击New SSH key添加秘钥，将刚才复制的test.pub复制到key位置处，Title可以写test，然后点击Add SSH key

![image-20240428040710945](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428040710945.png)

![image-20240428041033913](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428041033913.png)

下面是添加好的界面：

![image-20240428041133621](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428041133621.png)

5.现在可以回到之前的那个项目（仓库）。

然后选择SSH进行复制。

![image-20240428041327240](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428041327240.png)

6.进行克隆

```shell
git clone ssh # 进行仓库的本地克隆（如果提示Permission denied (publickey).请尝试ssh-add ~/.ssh/你的秘钥名称）
#这样就克隆完成了
```



分支（branch）：每次提交生成一个新版本的时候，都会生成一个提交对象，每一个提交对象都会有一个独一无二的哈希值，那其实分支就是一个包含这个哈希值的一个文件，可以简单的理解成指向一个提交对象的指针，也就是说可以在一个提交对象上新建多个分支，因为分支是包含这个提交对象哈希值的一个文件，所以想加多少就加多少。其实最开始初始化本地仓库的时候就已经新建了一个master分支（现在叫做main），每次提交操作都是在这个master分支上进行的，当每次进行一个提交的时候，我们的分支也跟着提交对象一起向前的移动。加入现在我们重新在这个第二次提交对象上新建一个分支，然后我们在master分支上进行一定的修改，然后提交一个新的提交对象，接下来在刚才新建的那个分支上也做一个修改，然后提交，这时候就发现第二次提交对象上分出了两个叉，这两个叉就是两个分支，这也就是分支的一个概念。

为啥要有多个分支，而不是一个分支？

![image-20240428044038813](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428044038813.png)

feature：开发一些新特性的时候是在feature上开发的。
develop：多个feature分支合并到develop分支，就是收集不同的feature分支，然后进行测试的。

release：测试没啥问题，功能都已经验证完成了，这时候就可以准备发布了，然后就可以新建ralease分支，

hot fixes：是用来修复bug用的。

master：发布版的一个分支。软件发不完新版本，经过向往验证也没有问题，然后就可以考虑把这个release分支合并到master分支里。



如何操作分支：

操作分支之前需要知道在那个分支上。

```shell
git log # 查看日志里面的分支
# commit哈希值后面的括号，下面的图表示现在在mast分支上，origin/master代码远程仓库上的master分支（就是远程分支在本地的副本），head表示现在所处的分支在master分支上。
```

![image-20240428044933500](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428044933500.png)

```shell
git status	# 也可以查看在哪个分支上
# 下面的图表示现在在master分支上
```

![image-20240428045249853](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428045249853.png)

```shell
git branch --list # 也可以查看现在在哪个分支上
# 前面带*就是表示现在在哪个分支上
```

![image-20240428045455927](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428045455927.png)

```shell
git branch 分支名字	# 创建分支
git branch --list # 查看分支
git checkout 要切换的分支名字 # 切换分支（现在有的是switch了）（checkout也可以恢复文件）
git add	# 提交
git commit -a -m '分支名字' # 把没有暂存的文件也提交了
git log --pretty=oneline	# 查看提交信息
```

```shell
git checkout -b 分支名字	# 新建一个分支，并且切换到这个分支 -b表示切换
```

```shell
git log --all	# 查看所有分支的提交
git log --all --graph # 查看所有分支的提交，可以看清楚分支情况，提交之后就分支就延伸出去了（按q退出）
```

```shell
git	merge 要合并的分支名字 # 合并分支 (将分支合并到master分支上) （要合并的分支是master分支上分出去的）
```

```shell
git push origin master(分支)	# 推送到master分支
git push -u origin master(分支)	# 这样推送一次之后，以后每次推送到master分支直接git push就可以了，不用写push后面的
```

```shell
git fetch	# 拉取远程仓库的内容（换一个本地没有上面内容的仓库）
```

```shell
# 新建跟踪分支：3种写法
git checkout 远程分支名字	# 切换到远程分支，把远程分支变为了本地分支
git checkout -b 跟踪分支名字 远程分支名字	# 确切的说是建立了远程分支的跟踪分支
git checkout -b featurel origin/feature1
git checkout --track 远程分支名字(origin/feature1)	# 新建跟踪分支
```



贮藏（stash）:

一般写代码写到一半的时候，然后线上有个bug需要赶紧去修改，这时候checkout不到master分支，因为现在还有东西没有写完，也就是说现在工作目录是脏的，有一个不推荐的写法就是把写在写到一半的功能进行一个提交，这个时候有一个命令git stash来贮藏我们当前所修改的东西，git stash等价于git stash push这个命令，向切换到哪里都可以。

实际操作：

![image-20240428130915577](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428130915577.png)

![image-20240428130930601](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428130930601.png)

当切换分支，修改完bug之后，再切换到之前自己写的分支，使用git stash apply来恢复刚才存储的内容。

```shell
git stash apply	# 恢复刚才存储的内容
```

![image-20240428131222707](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428131222707.png)

git stash不光可以存储一次，还可以存储多次。

再次存储：

![image-20240428171853083](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428171853083.png)

![image-20240428171931157](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428171931157.png)

```shell
git stash list	# 查看存储的东西
```

查看存储的东西：

![image-20240428172040876](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428172040876.png)

总共存储了3次，这个0就是最后存储的一次东西，1是上一次存储的，2是最开始存储的。

```shell
git stash apply stash@{2}	# 恢复第一次存储的东西
```

恢复第一次存储的东西：

![image-20240428172400457](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428172400457.png)

在一个不干净的目录里，再次apply一次，加入目录不干净的话是无法再次apply的。

![image-20240428172533410](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428172533410.png)

![image-20240428172648921](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428172648921.png)

```shell
# 如何撤销修改？
# 情况1：在工作区已修改，但并未提交到暂存区（即并没有add）
git checkout -- 文件名	# 撤销单个文件修改
git checkout .	# 撤销工作区中所有文件的修改
# 注意：git checkout是让文件回到最近一次该文件git commit或it add时的状态

# 情况2：工作区修改了之后，提交到了暂存区（即add），如何撤销修改？
# 2.1使用git status查看结果文件还没有conmmit过。
git rm --cached 文件名	# 先放弃该文件的暂存
# 然后使用git commit查看结果文件已近被修改，没有提交到暂存区，不被git跟踪，这时候使用情况1的解决方法是没有用的。
# 这时使用情况1的解决办法，会报错：该文件在Git目前所知的文件中找不到。此时你可以任意的对此文件进行修改，再提交到暂存区。
# 2.2对于撤销的文件，已经有了commit的记录。

git reset HEAD file	# 撤销暂存区中文件的修改，让文件回到工作区的状态。（回到上一个节点）
git checkout -- file # 
# 总结：
git checkout -- 文件名 # 撤销工作中文件的修改
git reset HEAD 文件名 # 撤销暂存区中文件的修改

```

```shell
推荐博客地址（更加详细的撤销）：https://blog.csdn.net/weixin_44137575/article/details/107661859?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-107661859-blog-109280534.235%5Ev43%5Epc_blog_bottom_relevance_base7&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-107661859-blog-109280534.235%5Ev43%5Epc_blog_bottom_relevance_base7&utm_relevant_index=1
```

除了git stash apply，还可以使用git cehckout -- 文件名。

把这个文件恢复成没有修改的状态，这个功能不要轻易使用，因为用了这个命令，所有的修改就都没了，这个是无法找回的，文件里的修改就没有了。接下来使用git stash pop来把最后一次存储的stash恢复。（pop有一定的副作用，就是最后一次恢复的stash会在恢复完成之后直接删掉）

![image-20240428180109318](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428180109318.png)

git stash list结果：

![image-20240428180308417](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428180308417.png)

想直接删除别的话，也可以使用git stash drop stash@{0}，就把最后一次存储的stash删除了。（里面的数字可以变）

![image-20240428180413335](C:\Users\19827\AppData\Roaming\Typora\typora-user-images\image-20240428180413335.png)

删除之后stash@{1}不见了，stash@{0}还在。

是因为是一个往前顺延的，把0删除了，后面的1就变成了0了。



重置（reset）：

```shell
git reset head~ --soft	# 可以撤销提交
# 有~表示祖先，表示上次，也有head~3这种写法表示倒数第3次
# sotf表示现在只是撤销提交，也就是撤销commit操作，之前git add把文件设置成暂存状态的这个状态还是存在的
# 不加sotf选项表示这个暂存状态是没有的，但是上次修改的代码还是存在的，这时候只需要git add把它加到暂存区，再使用commit再次提交，和之前也没有什么区别
# 除了sotf还有一个hard选项，表示不光把暂存取消了，而且把之前修改的那些内容也取消了，就彻底回到了上一次刚提交完的一个状态。（这个hard不推荐使用，因为会丢失数据，修改的东西会没了）
```



变基（rebase）：

可以理解为搬家，比如有两个分支a和b，可以使用合并的操作，也可以使用变基的操作，在这个场景下，两个的功能是一样的，只不过变基这个操作可以让提交记录变得好看一写，在b分支git rebase a就会把b分支上的修改移动到a分支上面。

注意事项：假设你的分支已经提交到了远程分支上，别人拿你的分支去进行二次开发，这时候自己的分支就不要再进行变基了。这就好像自己盖了一层楼，同事接着在自己的远程分支上盖第二层但这时候自己把自己的分支变了基；等同事开发完了，就好像盖了两层楼，同事突然发现第一层没了，这就很尴尬。

rebase还有一个最强大的功能，交互式操作。

```shell
 git rebase -i head~3	# 选择了前三次提交的一个分支进行编辑，对前三个提交进行一个修改，按下回车之后进入到一个交互式的界面（这个操作很强大，新手不要随便使用，使用的时候要先多查询进行测试练习）
```





# 3.git学习的书籍

git官方书籍和文档：[Git - Book (git-scm.com)](https://git-scm.com/book/zh/v2)

github官方文档：[开始你的旅程 - GitHub 文档](https://docs.github.com/zh/get-started/start-your-journey)

vscodoGUI工具的git:[Source Control with Git in Visual Studio Code](https://code.visualstudio.com/docs/sourcecontrol/overview)

IDEAGUI工具de git:[Set up a Git repository | IntelliJ IDEA Documentation (jetbrains.com)](https://www.jetbrains.com/help/idea/set-up-a-git-repository.html)



# 4.如何看别人的github项目

git clone：克隆仓库，下载到本地。

Star：收藏，收藏的人越多说明这个项目的可靠度越高。

README.md：一个项目的介绍。

LICENSE：项目的许可、证书。

issue：项目讨论的地方。



# 5.如何在github上找开源项目

https://github.com/trending/

https://github.com/521xueweihan/HelloGitHub

https://github.com/raunyf/weekly

https://www.zhihu.com/column/mm-fe



# 6.在github上查找资源的小技巧

找百科大全：awesome xxx

找例子：xxx sample

找空项目架子：xxx starter / xxx boilerplate

找教程：xxx tutorial



# 7.基本命令

```shell
git add -A	# 把工作区的内容添加到暂存区
git commit -m "提交信息" # 把暂存区的内容添加到远程仓库，并且对提交的内容进行备注
git init # 初始化
git log --stat	# 查看提交的历史
```

```shell
# 维护项目的日常
git checkout <filename> # 工作区打回去
git reset HEAD^数字 # 提交后撤回（数字表示撤销几步），之后就回到工作区了，再使用checkout就可以了
```

```shell
# 分支 目的是多人协作
git checkout -b <branchname>	# 从当前节点新建分支
git branch	# 列举所有的分支
git checkout <branchname> # 单纯地切换到某个分支
git checkout -D <branchname> # 删掉特定的分支（-D是强制删除，-d是删除）
git merge <branchname> # 合并分支
git merge --about # 放弃这次合并，找能处理这次冲突的同事来处理冲突
```

```shell
# 把已有的仓库提交到远程仓库
git remote add origin 远端仓库(https)	# 把远端仓库添加到了本地的地址中
git branch -M main	# 把本地的master改名为main
git push -u origin main	# 把本地的推送到远端仓库中（这里会有一个弹窗要认证，点击会进入浏览器或者输入ssh的token）
```

```shell
git push	#推送当前分支最新的提交到远程
git pull	#拉取远程分支最新的提交到本地
```

注意事项：本地远程双向更新：先pull后push



``` shell
git clone ssh	# 把远程仓库克隆到本地
git brnach -vv # 查看本地对应远程的分支对应关系
git branch -a # 查看本地和远程所有分支
git checkout -b 分支名字 # 以当前本地分支为基础新建一个本地分支
git push origin 分支名字 # push到分支名字
git branch --set-upstream-to=origin/远程分支	# 将本地分支与远程分支进行关联形成关联关系
git status # 查看git仓库中文件的状态
git diff # 比较工作区中的文件与暂存区中的文件差异
git add . # 将所有代码提交到到暂存区
git commit -m "备注信息" # 用于将当前工作目录中的修改提交到本地代码库中，并添加一个备注信息。（本地仓库比较抽象）
git push # 将本地仓库的更新推送到远程仓库
git pull # 拉取最新远程代码
git mrege 目标分支	# 将目标分支合并到当前分支(注意：git merge前一定要git push,之后也要git push)（git合并的分支不会在合并之后丢失）
git checkout 要切换的分支	# 切换分支
git checkout .	# 修改的部分代码清理掉不修改了，就是修改之后不想要修改的，把之前的代码拉取覆盖。（注意：这个操作是在没有add之前才有用的）
git branch --set-upstream-to=origin/远程分支	# 将本地分支与远程分支进行关联形成关联关系
git branch -d 要删除的分支	# 删除分支，当前分支不能是要删除的分支
git push origin --delete 要删除的远程分支	# 删除远程分支
git reset HEAD . # 撤销所有已经add的文件
git reset --mixed # 文件退出暂存区，但是修改
git reset HEAD 文件名字 # 撤销某个文件或文件夹
git reset --soft HEAD^ # git commit之后悔了（撤销commit之后返回暂存区add的状态）
git reset --hard HEAD^ # 撤销commit，代码全部撤销并没有add暂存直接消失（这个命令能不用不要用，是补救时候使用的）
git stash save "备注"	#贮藏已近修改的代码
git stash list # 查看贮藏的修改
git stash pop stash@{1} # 释放贮藏内容到当前分支
git config --list # 查看这个项目的git配置
git log # 查看最近的提交信息
git log --graph --oneline # 以图标的形式展示最近的提交信息
git reset --hard （git log查询出来的哈希值） # 回退到某一个历史接节点(注意点：回退之后要git push -f强制提交)（这个命令不要随便使用，会丢失工作区文件）
git push -f # 强制提交(-f表示强制)
```



# 8.插件

gitLens

Git history diff

