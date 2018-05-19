#CoreData

[参考链接](https://www.jianshu.com/p/c0e12a897971)

### 主要的几个类
> NSPersistentStoreCoordinator(持续化储存器)
>>储存在磁盘上的数据库

> NSManagedObjectContext(托管对象上下文)

> NSManagedObjectModel (管理模型对象)
> > 数据模型

> NSManagedObject（托管对象）
> 
> NSEntityDescription (实体对象)
> NSFetchRequest (为获取结构控制器而修改对象)
> 
> NSFetchedResultsController (coreData来展示拉取数据和展示给用户的控制器)
> 
> NSSortDescriptor (数据对象进行排序， 升序或者降序)
### 属性
> sections:(Array 类型)
> 对数据进行分组
>
> objectAtIndexPath:(实体方法，返回一个实例对象)
> #####例如
> ````
>     NSManagedObject* obj = [self.fetchController  objectAtIndexPath:path];
     [self.managedContext deleteObject:obj];
     
> ````
> 
> 
### NSFetchedResultsControllerDelegate
> controllerWillChangeContent: 获取结果的控制器context发生变化，并做出相应的改变
> 
> controller: didChangeObjcet:atIndexPath:forChangeType:newIndexPath:
> context中的某个对象发生了改变
> 
> controllerDidChangeContent:
>  


### 创建结构控制器
> ````
> - (NSFetchedResultsController *)fetchController
> {
    if (_fetchController != nil) {
        return _fetchController;
    }
    
>    NSFetchRequest *fetchRequest = [[NSFetchRequest alloc] init];
    // Edit the entity name as appropriate.
    NSEntityDescription *entity = [NSEntityDescription entityForName:self.entityName inManagedObjectContext:self.managedContext];
    [fetchRequest setEntity:entity];
    
>    // Set the batch size to a suitable number.
    [fetchRequest setFetchBatchSize:20];
    [fetchRequest setPredicate:self.predicate];
    
>    // Edit the sort key as appropriate.
    NSSortDescriptor *sortDescriptor = [[NSSortDescriptor alloc] initWithKey:self.sortKey ascending:self.ascending];
    NSArray *sortDescriptors = @[sortDescriptor];
    
>   [fetchRequest setSortDescriptors:sortDescriptors];
    
>    // Edit the section name key path and cache name if appropriate.
    // nil for section name key path means "no sections".
    _fetchController= [[NSFetchedResultsController alloc] initWithFetchRequest:fetchRequest managedObjectContext:self.managedContext sectionNameKeyPath:nil cacheName:nil];
    _fetchController.delegate = self;
    
>   NSError *error = nil;
    if (![_fetchController performFetch:&error]) {
        // Replace this implementation with code to handle the error appropriately.
        // abort() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
        ////LOGMARK(@"Unresolved error %@, %@", error, [error userInfo]);
        abort();
    }
    
>    return _fetchController;
}
```

### 主要流程图
![](https://upload-images.jianshu.io/upload_images/270478-31111e004bcb9c88.png)  








