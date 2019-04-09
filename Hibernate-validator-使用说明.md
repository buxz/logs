---
title: Hibernate validator 使用说明
date: 2019-03-05 09:54:09
tags:
---

# @NotNull和@NotEmpty和@NotBlank区别
1. @NotNull: 不能为null, 但可以为empty
2. @NotEmpty: 不能为null,而且长度必须大于0
3. @NotBlank: 只可以作用在String上，不能为null,而且调用trim()后，长度大于0
```
String name = null
@NotNull : false
@NotEmpty : false
@NotBlank : false

String name = "";
@NotNull : true
@NotEmpty : false
@NotBlank : false

String name = " ";
@NotNull : true
@NotEmpty : true
@NotBlank : false

String name = "hello ";
@NotNull : true
@NotEmpty : true
@NotBlank : true
```
