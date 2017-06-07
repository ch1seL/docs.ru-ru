---
title: "Действия с сущностями | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c04f7413-7fb8-40c6-819e-dc92b145b62e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Действия с сущностями
В этом образце показывается, как можно использовать платформу ADO.NET Entity Framework совместно с [!INCLUDE[wf2](../../../../includes/wf2-md.md)] для упрощения доступа к данным.  
  
 С помощью платформы ADO.NET Entity Framework разработчики могут работать с данными в форме объектов, свойств и связей определенного домена, например клиентов, заказов, подробных сведений о заказах и связей между этими сущностями.В платформе ADO.NET Entity Framework это достигается за счет уровня абстракции, позволяющего осуществлять программирование по концептуальной модели приложения, а не напрямую по схеме реляционного хранилища.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] платформе ADO.NET Entity Framework см. в разделе [ADO.NET Entity Framework](http://go.microsoft.com/fwlink/?LinkId=165549).  
  
## Подробные сведения об образце  
 В этом образце используется база данных `Northwind`, в него входят скрипты для создания и удаления базы данных `Northwind` \(Setup.cmd и Cleanup.cmd\).Среди проектов этого образца имеется модель EDM, основанная на базе данных `Northwind`.Модель можно найти, открыв файл `Northwind.edmx`, который включен в проект.Именно эта модель определяет форму объектов, к которым может осуществляться доступ из платформы ADO.NET Entity Framework.  
  
 В данный образец включены следующие действия:  
  
-   `EntitySQLQuery`: действие `EntitySQLQuery` позволяет получать объекты из базы данных на основе строки запроса Entity SQL.Entity SQL — это независимый от хранилища язык, сходный с SQL, который позволяет задавать запросы на основе концептуальной модели и сущностей, являющихся частью модели или домена.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] о языке Entity SQL см. в разделе [Язык Entity SQL](http://go.microsoft.com/fwlink/?LinkId=165646).  
  
-   `EntityLinqQuery`: это действие позволяет получать объекты из базы данных на основе запроса LINQ или предиката.  
  
-   `EntityAdd`: действие `EntityAdd` позволяет добавлять сущность или коллекцию сущностей в базу данных.  
  
-   `EntityDelete`: действие `EntityDelete` позволяет удалять сущность или коллекцию сущностей из базы данных.  
  
-   `ObjectContextScope`: упомянутые ранее действия могут быть использованы только в пределах содержащего их экземпляра действия `ObjectContextScope`.Действие `ObjectContextScope` настраивает соединение с базой данных.Для действия требуется строка подключения \(которая передается с использованием настройки файла конфигурации или возвращается с ее помощью\).Действие `ObjectContextScope` облегчает выполнение группы связанных операций с сущностями.Поскольку эта область поддерживает активное соединение, она является несохраняемой областью.Кроме того, при выполнении действием `ObjectContextScope` выхода все изменения, которые внесены в объекты, возвращенные с помощью действий сущностей в области, автоматически сохраняются в базе данных. Для сохранения объектов в базу данных не требуется никаких последующих действий.  
  
## Использование действий сущностей  
 Следующие фрагменты кода демонстрируют использование действий сущностей, представленных в этом образце.  
  
### EntitySql  
 Приведенный далее фрагмент кода показывает, как запрашивать всех клиентов из Лондона с сортировкой по имени и как выполнить итерацию по списку клиентов.  
  
```  
Variable<IEnumerable<Customer>> londonCustomers = new Variable<IEnumerable<Customer>>();  
DelegateInArgument<Customer> iterationVariable = new DelegateInArgument<Customer>();  
  
// create and return the workflow  
return new ObjectContextScope  
{  
    ConnectionString = new InArgument<string>(connStr),  
    ContainerName = "NorthwindEntities",  
    Variables = { londonCustomers },  
    Body = new Sequence  
        {  
            Activities =   
                {               
                    new WriteLine { Text = "Executing query" },                            
                    // query for all customers that are in london   
                    new EntitySqlQuery<Customer>  
                    {  
                        EntitySql =  @"SELECT VALUE Customer   
                                        FROM NorthwindEntities.Customers AS Customer   
                                        WHERE Customer.City = 'London'   
                                        ORDER BY Customer.ContactName",  
                        Result = londonCustomers  
                    },  
  
                    // iterate through the list of customers and display them   
                    new ForEach<Customer>  
                    {                                      
                        Values = londonCustomers,  
                        Body = new ActivityAction<Customer>  
                        {  
                            Argument = iterationVariable,  
                            Handler = new WriteLine   
                            {   
                                  Text = new InArgument<String>(e =>    
                                              iterationVariable.Get(e).ContactName)   
                            }  
                        }  
                    }  
                }  
        }                 
};  
  
```  
  
### EntityLinqQuery  
 Приведенный далее фрагмент кода показывает, как запросить всех клиентов из Лондона и как выполнить итерацию по итоговому списку клиентов.  
  
```  
Variable<IEnumerable<Customer>> londonCustomers = new Variable<IEnumerable<Customer>>() { Name = "LondonCustomers" };  
DelegateInArgument<Customer> iterationVariable = new DelegateInArgument<Customer>() { Name = "iterationVariable" };  
  
return new ObjectContextScope  
{  
    ConnectionString = new InArgument<string>(connStr),  
    ContainerName = "NorthwindEntities",  
    Variables = { londonCustomers },  
    Body = new Sequence  
    {  
        Activities =   
        {               
            // return all the customers that match with the provided Linq predicate  
            new EntityLinqQuery<Customer>  
            {   
                Predicate = new LambdaValue<Func<Customer, bool>>(  
                          ctx => new Func<Customer, bool>(c => c.City.Equals("London"))),                              
                Result = londonCustomers  
            },  
  
            // iterate through the list of customers and display in the console  
            new ForEach<Customer>  
            {                                      
                Values = londonCustomers,  
                Body = new ActivityAction<Customer>  
                {  
                    Argument = iterationVariable,  
                    Handler = new WriteLine   
                    {   
                        Text = new InArgument<String>(e =>   
                                      iterationVariable.Get(e).ContactName)   
                    }  
                }  
            }  
        }  
    }  
};  
  
```  
  
### EntityAdd  
 Приведенный далее фрагмент кода показывает, как добавить запись OrderDetail в существующий заказ.  
  
```  
Variable<IEnumerable<Order>> orders = new Variable<IEnumerable<Order>>();  
Variable<IEnumerable<OrderDetail>> orderDetails = new Variable<IEnumerable<OrderDetail>>();  
Variable<Order> order = new Variable<Order>();  
Variable<OrderDetail> orderDetail = new Variable<OrderDetail>();              
  
return new ObjectContextScope  
{  
    Variables = { order, orders, orderDetail, orderDetails },  
    ContainerName = "NorthwindEntities",  
    ConnectionString = new InArgument<string>(connStr),                  
    Body = new Sequence  
    {                      
        Activities =   
        {                            
           // get the order where we want to add the detail  
           new EntitySqlQuery<Order>  
           {  
               EntitySql =    
                    @"SELECT VALUE [Order]  
                      FROM NorthwindEntities.Orders as [Order]  
                      WHERE Order.OrderID == 10249",  
               Result = orders  
           },  
  
           // store the order in a variable  
           new Assign<Order>   
           {  
               To = new OutArgument<Order>(order),  
               Value = new InArgument<Order>(c => orders.Get(c).First<Order>())  
           },  
  
           // add the detail to the order  
           new EntityAdd<OrderDetail>  
           {  
               Entity = new InArgument<OrderDetail>(c =>   
                                         new OrderDetail {   
                                                  OrderID=10249, ProductID=11,   
                                                  Quantity=1, UnitPrice = 15,   
                                                  Discount = 0, Order = order.Get(c) })  
           }  
        }  
    }  
};  
  
```  
  
### EntityDelete  
 Приведенный далее фрагмент кода показывает, как удалить существующую запись OrderDetail из заказа \(если он существует\).  
  
```  
Variable<IEnumerable<OrderDetail>> orderDetails = new Variable<IEnumerable<OrderDetail>>();              
  
return new ObjectContextScope  
{  
    Variables = { orderDetails },  
    ConnectionString = new InArgument<string>(connStr),  
    ContainerName = "NorthwindEntities",  
    Body = new Sequence  
    {  
        Activities =   
        {               
            // find the entitiy to be deleted (order detail for product 11 in order 10249)  
            new EntitySqlQuery<OrderDetail>  
            {  
                EntitySql = @"SELECT VALUE OrderDetail  
                                FROM NorthwindEntities.OrderDetails as OrderDetail  
                               WHERE OrderDetail.OrderID == 10249   
                                 AND OrderDetail.ProductID == 11",  
                Result = orderDetails  
            },  
  
            // if the order detail is found, delete it, otherwise, display a message  
            new If  
            {  
                Condition = new InArgument<bool>(c=>orderDetails.Get(c).Count() > 0),  
                Then = new Sequence  
                {   
                    Activities =   
                    {                                      
                        new EntityDelete<OrderDetail>  
                        {  
                            Entity = new InArgument<OrderDetail>(c =>   
                                              orderDetails.Get(c).First<OrderDetail>())  
                        },  
                    }  
                },                              
                Else = new WriteLine { Text = "Order Detail for Deleting not found" }                              
            }                                                  
        }  
    }  
};  
  
```  
  
## Использование этого образца  
 Перед выполнением этого образца необходимо создать базу данных `Northwind` в локальном экземпляре SQL Server Express.  
  
#### Настройка базы данных «Northwind».  
  
1.  Откройте окно командной строки.  
  
2.  В новом окне командной строки перейдите в папку EntityActivities\\CS.  
  
3.  Введите `setup.cmd` и нажмите клавишу ВВОД.  
  
#### Выполнение образца  
  
1.  Откройте файл решения EntityActivities.sln в среде [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Для построения решения нажмите CTRL\+SHIFT\+B.  
  
3.  Чтобы запустить решение, нажмите клавиши CTRL\+F5.  
  
 После выполнения этого образца базу данных `Northwind` можно удалить.  
  
#### Удаление базы данных «Northwind».  
  
1.  Откройте окно командной строки.  
  
2.  В новом окне командной строки перейдите в папку EntityActivities\\CS.  
  
3.  Введите `cleanup.cmd` и нажмите клавишу ВВОД.  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере.Перед продолжением проверьте следующий каталог \(по умолчанию\).  
>   
>  `<диск_установки>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Образцы Windows Communication Foundation \(WCF\) и Windows Workflow Foundation \(WF\) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780), чтобы загрузить все образцы [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Этот образец расположен в следующем каталоге.  
>   
>  `<диск_установки>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\EntityActivities`  
  
## См. также