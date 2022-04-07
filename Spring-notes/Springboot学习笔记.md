# 1、spring boot之rest风格

## 1） rest风格中常用注释

### @GetMapping

用于将HTTP GET请求映射到特定处理程序方法的注释。具体来说，@GetMapping是一个作为快捷方式的组合注释
@RequestMapping(method = RequestMethod.GET)。

### @PostMapping

用于将HTTP POST请求映射到特定处理程序方法的注释。具体来说，@PostMapping是一个作为快捷方式的组合注释@RequestMapping(method = RequestMethod.POST)。

### @RequestMapping:

一般情况下都是用@RequestMapping（method=RequestMethod.），因为@RequestMapping可以直接替代以上两个注解，但是以上两个注解并不能替代@RequestMapping，@RequestMapping相当于以上两个注解的父类！