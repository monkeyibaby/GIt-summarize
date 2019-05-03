1、git init 初始化版本库
2、添加文件到Git仓库，分两步：
  使用命令git add <file>，注意，可反复多次使用，添加多个文件；
  该操作是将修改过的文件提交到暂存区，
  使用命令git commit -m <message>，完成。message为提交说明。
  该操作是将在暂存区的文件提交到版本库；
3、要随时掌握工作区的状态，使用git status命令。
  如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
  注解：Git warning：LF will be replaced by CRLF in readme.txt的原因与解决方案：
  问题出在不同操作系统所使用的换行符是不一样的，下面罗列一下三大主流操作系统的换行符：
  Uinx/Linux采用换行符LF表示下一行（LF：LineFeed，中文意思是换行）；
  Dos和Windows采用回车+换行CRLF表示下一行（CRLF：CarriageReturn LineFeed，中文意思是回车换行）；
  Mac OS采用回车CR表示下一行（CR：CarriageReturn，中文意思是回车）。
  Git中，可以通过以下命令来显示当前你的Git中采取哪种对待换行符的方式
      $ git config core.autocrlf
  此命令会有三个输出，“true”，“false”或者“input”
  true时，Git会将你add的所有文件视为文本问价你，
  将结尾的CRLF转换为LF，而checkout时会再将文件的LF格式转为CRLF格式。
  false时，line endings不做任何改变，文本文件保持其原来的样子。
  input时，add时Git会把CRLF转换为LF，而check时仍旧为LF，所以Windows操作系统不建议设置此值。
  解决办法：
  将core.autocrlf设为false即可解决这个问题，不过如果
  你和你的伙伴只工作于Windows平台或者Linux平台，那么没问题，
  不过如果是存在跨平台的现象的话，还是需要考虑一下。
  但当 core autocrlf为true时，还有一个需要慎重的地方，
  当你上传一个二进制文件，Git可能会将二进制文件误以为是文本文件，
  从而也会修改你的二进制文件，从而产生隐患。
  PS:
  附上修改autocrlf的命令，以改为true为例：
  $ git config --global core.autocrlf true   
  #true的位置放你想使autocrlf成为的结果，true，false或者input
4、git log命令显示从最近到最远的提交日志，
   首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，
   也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），
   上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，
   所以写成HEAD~100。
    现在，我们要把当前版本append GPL回退到上一个版本add distributed，就可以使用git reset命令：
       $ git reset --hard HEAD^  //命令 git reset --hard head~*/指定版本号（*代表上多少个版本）
       HEAD is now at e475afc add distributed
       HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，
       使用命令git reset --hard commit_id。
    穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
    要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
5、命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，
   这里有两种情况：
   （1）是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
   （2）一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
   总之，就是让这个文件回到最近一次git commit或git add时的状态。
6、命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区   
7、将本地仓库推送到远程仓库：$ git remote add origin git@github.com:monkeyibaby/IFE2018.git
        $ git remote add origin git@github.com:（用户名）/仓库名.git
	$ git push -u origin master
	关联成功后使用git push origin master
	将远程仓库克隆到本地仓库：
	$ git clone git@github.com:（用户名）/仓库名.git

