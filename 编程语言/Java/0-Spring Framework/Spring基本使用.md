### Bean加载后执行初始化操作

> 构造器中添加业务逻辑
>
> 添加`@PostConstruct`注解
>
> 实现`InitializingBean`接口，实现`afterPropertiesSet`方法。
>
> 使用xml 或者`@Bean`注解中的init-method
>
> 实现`ApplicationContextL

三种的执行先后顺序 ：构造器  > PostContruct > afterPropertiesSet > initMethod

