---
title: "coredump配置"
date: 2023-06-18T14:05:25+08:00
tags: ["编译调试"]
categories: []
draft: false
toc: true
---
```bash
ulimit -c unlimited
echo "1" > /proc/sys/kernel/core_uses_pid
mkdir -p /opt/debug
echo "/opt/debug/core-%e-%p-%t" > /proc/sys/kernel/core_pattern


gdb <program> -c <coredump_file>
up <n> #调用栈向上n次
```