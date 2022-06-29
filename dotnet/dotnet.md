## SOLID原则

- [单一责任原则(SRP)](https://www.dotnetcurry.com/software-gardening/1148/solid-single-responsibility-principle)

  方法不要太面向过程化。将主要功能细化

- [开放封闭原则(OCP)](https://www.dotnetcurry.com/software-gardening/1176/solid-open-closed-principle)

  不要修改原有的类。重新实现原有类接口，在新的类中拓展

- [里氏替换原则(LSP)](https://www.dotnetcurry.com/software-gardening/1235/liskov-substitution-principle-lsp-solid-patterns)

  继承中对不符合使用的方法和属性进行重写。多使用虚方法。

- [接口分离原则(ISP)](https://www.dotnetcurry.com/software-gardening/1257/interface-segregation-principle-isp-solid-principle)

  通用的业务定义通用的接口，不同的业务定义不同的接口。

- [依赖倒置原则(DIP)](https://www.dotnetcurry.com/software-gardening/1284/dependency-injection-solid-principles)

  通过接口进行声明，通过DI进行注入