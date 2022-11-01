# git

## Clone

```
$ git clone https://gitlab.com/MAZE-dankook/self-driving-patrol-car.git
```

## Branch

### check branch

```
$ git branch -a
or
$ git branch -r
```

### branch update 

```
$ git remote update
```

### branch checkout

```
$ git checkout <branch name>
$ git branch -a
```

## Pull

### git pull to rocal

```
$ git pull
```

## Commit

### check rocal status

```
$ git status
```

### commit to rocal

```
$ git add <file name>
or
$ git add .
```

### reset commit

```
$ git reset (add 삭제)
$ git reset HEAD^ (가장최근 commit)
```

### commit message

```
$ git commit -s
$ git commit --amend (modifying)
```

## Push

### git push to server

```
$ git push
$ git push --force-with-lease (commit 강제 수정)
```
