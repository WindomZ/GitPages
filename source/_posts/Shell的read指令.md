---
title: Shell的read指令
date: 2017-06-27 20:18:14
tags:
  - Linux
  - Shell
  - Bash
---

我们经常在脚本中会涉及交互输入，`read`则是最常用的命令，并且shell基本都能支持。

不过不同版本会有差异，比较常用的是`-t`等待时间，`-p`提示语句，`-s`隐藏输入，`-d`分界符。

`read`可以接受管道和重定向输入。

## read命令

> 接收标准输入(键盘)的输入，或文件描述符的输入(使用句柄)，并将其拆分赋值。

- -a array 数组
    - assign the words read to sequential indices of the array variable ARRAY, starting at zero
    - 将读取的内容按照从零开始顺序赋值给数组变量ARRAY

- -d delim 分界符
    - continue until the first character of DELIM is read, rather than newline
    - 读取的内容到分界符DELIM之前为止，不是换行，但常用换行作为分界符

- -e
    - use Readline to obtain the line in an interactive shell
    - 在shell交互脚本，使用`Readline`读取输入行，适用于使用`-i`等

- -i text 文本
    - Use TEXT as the initial text for Readline
    - 使用`Readline`读取输入行，在开始输入之前将文本TEXT写入输入区，适用于默认输入值

- -n nchars 字符个数
    - return after reading NCHARS characters rather than waiting for a newline, but honor a delimiter if fewer than NCHARS characters are read before the delimiter
    - 在读取NCHARS个字符后结束输入，而不是等待换行符；但是如果在分隔符之前读取少于NCHARS个字符，则遵循分隔符

- -N nchars 字符个数
    - return only after reading exactly NCHARS characters, unless EOF is encountered or read times out, ignoring any delimiter
    - 只有在读完NCHARS个字符后，才会结束输入，除非遇到EOF或读取超时，并且忽略任何分隔符

- -p prompt 提示语句
    - output the string PROMPT without a trailing newline before attempting to read
    - 在输入之前，写入没有换行符的字符串PROMPT作为提示输入信息，不占用输入

- -r
    - do not allow backslashes to escape any characters
    - 不允许反斜杠`\`作为转义符使用，例如禁用了`\`来表示没有未输入完成，换行继续输入

- -s
    - do not echo input coming from a terminal
    - 不显示输入内容，例如用于输入密码等

- -t timeout 超时时间
    - time out and return failure if a complete line of input is not read withint TIMEOUT seconds. The value of the TMOUT variable is the default timeout. TIMEOUT may be a fractional number. If TIMEOUT is 0, read returns success only if input is available on the specified file descriptor. The exit status is greater than 128 if the timeout is exceeded
    - 如果在TIMEOUT秒后未完成输入，则作为超时返回，不会赋值。
        如果TIMEOUT为0，则不会超时。
        如果超时退出，退出状态码会大于128

- -u fd 文件句柄
    - read from file descriptor FD instead of the standard input
    - 从文件句柄中读取，而不是标准输入

## 参考

- [linuxcommand.org](http://linuxcommand.org/lc3_man_pages/readh.html)
