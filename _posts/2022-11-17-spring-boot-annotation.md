---
title: Spring Boot 注解
author: kai
date: 2022-11-17
category: spring
layout: post
---

# Sping Boot注解

## @EnableAutoConfiguration

  它自动配置类路径中存在的bean，并将其配置为运行方法。在Spring Boot 1.2.0发行版中减少了使用此批注，因为开发人员提供了该批注的代替方法，即 @SpringBootApplication 。

## @SpringBootApplication

  它是三个注解 @ EnableAutoConfiguration，@ ComponentScan，和 @Configuration 的组合。

## Spring MVC和REST注解

### @RequestMapping

用于映射网络请求。它具有许多可选元素，例如 consumes, header, method, name, params, path, produces和value。我们将其与类以及方法一起使用

{% highlight Java %}

@Controller
public class BooksController
{
    @RequestMapping("/computer-science/books")
    public String getAllBooks(Model model)
    {
        //application code
        return "bookList";
    }
}

{% endhighlight %}

#### @GetMapping

 它将 HTTP GET 请求映射到特定的处理程序方法。它用于创建提取的Web服务终结点，而不是使用 @RequestMapping(method = RequestMethod.GET)

#### @PostMapping

 它将 HTTP POST 请求映射到特定的处理程序方法。它用于创建创建的Web服务终结点，而不是使用: @RequestMapping(method = RequestMethod.POST)

#### @PutMapping

 它将 HTTP PUT 请求映射到特定的处理程序方法。它用于创建创建或更新的Web服务终结点，而不是使用: @RequestMapping(method = RequestMethod.PUT)

#### @DeleteMapping

 它将 HTTP DELETE 请求映射到特定的处理程序方法。它用于创建删除资源的Web服务终结点。使用它而不是使用: @RequestMapping(method = RequestMethod.DELETE)

#### @PatchMapping

 它将 HTTP PATCH 请求映射到特定的处理程序方法。使用它代替使用: @RequestMapping(method = RequestMethod.PATCH)

#### @RequestBody

 用于将HTTP请求与方法参数中的对象绑定。在内部，它使用 HTTP MessageConverters 转换请求的正文。当我们用 @RequestBody注解方法参数时，Spring框架会将传入的HTTP请求主体绑定到该参数。

#### @ResponseBody

 它将方法返回值绑定到响应主体。它告诉Spring Boot Framework将返回的对象序列化为JSON和XML格式。

#### @PathVariable

 用于从URI中提取值。它最适合RESTful Web服务，其中URL包含路径变量。我们可以在一个方法中定义多个@PathVariable。

#### @RequestParam

 用于从URL提取查询参数。也称为查询参数。它最适合Web应用程序。如果URL中不存在查询参数，则可以指定默认值。

#### @RequestHeader

 用于获取有关HTTP请求标头的详细信息。我们将此注解用作方法参数。注解的可选元素是名称，必填，值，defaultValue。 对于标题中的每个细节，我们应指定单独的注解。我们可以在一种方法中多次使用它

#### @RestController

 可以将其视为 @Controller 和 @ResponseBody 注解的组合。 @RestController注解本身使用@ResponseBody注解进行注解。无需使用@ResponseBody注解每个方法。

#### @RequestAttribute

 它将方法参数绑定到请求属性。它提供了从控制器方法方便地访问请求属性的方法。借助@RequestAttribute批注，我们可以访问服务器端填充的对象。
