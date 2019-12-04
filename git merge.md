<!--
 * @Author: 千铭天
 * @Date: 2019-10-31 11:37:21
 * @LastEditors: 
 * @LastEditTime: 2019-10-31 11:40:43
 * @Description:  
 -->
# git冲突-多人修改统一文件的同一位置

>浪漫天下\
2018.12.01 17:54:18\
字数 361\
阅读 1,959

## 一、git fetch 和 git pull 的区别

1、    git fetch <远程主机名> <远程分支名>:<本地分支名>

         git fetch origin master ：temp             //将远程仓库origin的master分支的

        git diff temp                    //比较本地代码和远程代码的区别    

        git merge temp               // 合并temp分支到本地的master分支

2、git pull <远程主机名> <远程分支名>:<本地分支名>

    //取回远程分支的更新，并直接与本地分支合并

区别：git  pull 可以看作是git fetch 和 git merge 两个步骤的集合。



## 二、多人协作，当他人修改文件后，后提交的必须先pull在合并，并且在合并的时候会出现冲突

1、当远程仓库的代码更新后，我们在push提交时会出现提交不了的情况，这时我们必须pull更新后的远程代码。但是在远程代码合并本地代码时发生CONFLICT冲突，这时需要我们手动解决冲突，最后再push提交到远程代码。

2、解决方法  ：

```git
git checkout  branch          //选择分支

git fetch origin master       //拉取远程更新代码（只拉取不合并），这里不能git pull （合并有冲突）

git rebase  origin/master   //查看conflict ，手动修改冲突 

git add  .

git rebase --continue       //add 后不需要git commit

git push origin
```


## 参考资料
1. [git冲突-多人修改统一文件的同一位置](https://www.jianshu.com/p/5e6c8ba3afa2)