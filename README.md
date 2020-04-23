# Snippets
常用代码块
代码块所在位置
~/Library/Developer/Xcode/UserData/CodeSnippets

将需要迁移的代码块拷贝至此目录，重启Xcode即可

# 描述
- Title:表示代码块的标题；
- Summary：表示代码块的描述信息；
- Platform：表示代码块可以使用的平台，默认即可；
- Language：表示代码块可以使用的语言平台；
- Completion：表示代码块的快捷方式；
- Availability: 表示代码块的使用范围；

# 常用代码块

## 属性
```
@property (nonatomic, strong) <#class#> <#object#>;
@property (nonatomic, copy) NSString *<#name#>;
@property (nonatomic, assign) <#class#> <#property#>;
@property (nonatomic,weak) id<<#protocol#>> <#delegate#>;
@property(nonatomic,copy) <#Block#> <#block#>;
```

## 单利
```
static <#SingleObject#> *singleInstance = nil;
+ (instancetype)sharedInstance {
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        if (singleInstance == nil) {
            singleInstance = [[self alloc]init];
        }
    });
    return singleInstance;
}

+ (instancetype)allocWithZone:(struct _NSZone *)zone {
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        singleInstance = [super allocWithZone:zone];
    });
    return singleInstance;
}

- (id)copyWithZone:(NSZone *)zone {
    return singleInstance;
}

- (id)mutableCopyWithZone:(NSZone *)zone {
    return singleInstance;
}
```

## 懒加载
```
//数组
- (NSMutableArray *)<#name#> {
    if (!_<#name#>) {
        _<#name#> = [[NSMutableArray alloc] init];
    }
    return _<#name#>;
}
// 字典
- (NSMutableDictionary *)<#name#> {
    if (!_<#name#>) {
        _<#name#> = [[NSMutableDictionary alloc] init];
    }
    return _<#name#>;
}
// 自定义
- (<#CustomClass#> *)<#name#> {
    if (!_<#name#>) {
        _<#name#> = [[<#CustomClass#> alloc] init];
    }
    return _<#name#>;
}
```

## UITableView创建
```
- (void)initWithTableView {
    // 去掉多余的cell
    self.tableView.tableFooterView = [UIView new];
    // 预估高度
    self.tableView.estimatedRowHeight = 100;
    // 分割线样式
    self.tableView.separatorStyle = UITableViewCellSeparatorStyleSingleLine;
    self.tableView.separatorColor = [UIColor lightGrayColor];
    self.tableView.separatorInset = UIEdgeInsetsMake(0,16, 0, 16);
    // 注册cell
    [self.tableView registerNib:[UINib nibWithNibName:[NSStringFromClass([<#Class#> class])] bundle:[NSBundle mainBundle]] forCellReuseIdentifier:<#@"cellID"#>];
}

- (UITableView *)tableView {
    if (!_tableView) {
        _tableView = [[UITableView alloc] initWithFrame:self.view.frame];
        _tableView.delegate = self;
        _tableView.dataSource = self;
        [self.view addSubview:_tableView];
    }
    return _tableView;
}

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    <#code#>
}

- (NSInteger)tableView:(nonnull UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    <#code#>
}

- (nonnull UITableViewCell *)tableView:(nonnull UITableView *)tableView cellForRowAtIndexPath:(nonnull NSIndexPath *)indexPath {
    <#code#>
}

- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath {
    <#code#>
}

- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
    <#code#>
}
```

## UICollectionView创建
```
- (UICollectionView *)collectionView {
    if (!_collectionView) {
        _collectionView = [[UICollectionView alloc] init];
        [self.view addSubview:_collectionView];
    }
    return _collectionView;
}

- (void)initWithCollectionView{
    self.collectionView.delegate = self;
    self.collectionView.dataSource = self;
    UICollectionViewFlowLayout *flowLayout = [[UICollectionViewFlowLayout alloc]init];
    // item大小
    flowLayout.itemSize = CGSizeMake(10, 10);
    // 每个section内缩进
    flowLayout.sectionInset = UIEdgeInsetsMake(10, 10, 10, 10);
    // 同一个section内部 item的水平方向间隙
    flowLayout.minimumLineSpacing = 5;
    // 同一个section内部间item的垂直方向的间距
    flowLayout.minimumInteritemSpacing = 5;
    self.collectionView.collectionViewLayout = flowLayout;
    [self.collectionView registerNib:[UINib nibWithNibName:NSStringFromClass([<#Class#> class]) bundle:[NSBundle mainBundle]] forCellWithReuseIdentifier:@"<#cellId#>"];
}

- (NSInteger)numberOfSectionsInCollectionView:(UICollectionView *)collectionView {
    <#code#>
}

- (NSInteger)collectionView:(UICollectionView *)collectionView numberOfItemsInSection:(NSInteger)section {
    <#code#>
}

- (UICollectionViewCell *)collectionView:(UICollectionView *)collectionView cellForItemAtIndexPath:(NSIndexPath *)indexPath {
    <#UICollectionViewCell#> *cell = [collectionView dequeueReusableCellWithReuseIdentifier:@"<#cellId#>" forIndexPath:indexPath];
    return cell;
}

- (void)collectionView:(UICollectionView *)collectionView didSelectItemAtIndexPath:(NSIndexPath *)indexPath {
    <#code#>
}
```
