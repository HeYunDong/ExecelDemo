# ExecelDemo
execel表格录入自适应高度

   //创建execel  
    _leftTableView = [[UITableView alloc] init];
    _leftTableView.delegate = self;
    _leftTableView.dataSource = self;
    _leftTableView.estimatedRowHeight = 50;
    _leftTableView.backgroundColor = [UIColor clearColor];
    _leftTableView.separatorStyle = UITableViewCellSeparatorStyleNone;
    _leftTableView.backgroundColor = [UIColor redColor];
    _leftTableView.showsVerticalScrollIndicator = NO;
    _leftTableView.showsHorizontalScrollIndicator = NO;
    [_leftTableView registerClass:[LeftTableViewCell class] forCellReuseIdentifier:@"LeftTableViewCell"];
    
    [self.view addSubview:_leftTableView];
    
    _rightTableView = [[UITableView alloc] init];
    _rightTableView.delegate = self;
    _rightTableView.dataSource = self;
    _rightTableView.estimatedRowHeight = 50;
    _rightTableView.backgroundColor = [UIColor clearColor];
    _rightTableView.separatorStyle = UITableViewCellSeparatorStyleNone;
    _rightTableView.backgroundColor = [UIColor blueColor];
    _rightTableView.showsVerticalScrollIndicator = NO;
    _rightTableView.showsHorizontalScrollIndicator = NO;
    [_rightTableView registerClass:[RightTableViewCell class] forCellReuseIdentifier:@"RightTableViewCell"];
    
    [_leftTableView addObserver:self forKeyPath:@"contentOffset" options:NSKeyValueObservingOptionNew|NSKeyValueObservingOptionOld context:nil];
    [_rightTableView addObserver:self forKeyPath:@"contentOffset" options:NSKeyValueObservingOptionNew|NSKeyValueObservingOptionOld context:nil];
    
    _rightContentView = [[UIView alloc] init];
    [_rightContentView addSubview:_rightTableView];

    _rightScrollView = [[UIScrollView alloc] init];
    [_rightScrollView addSubview:_rightContentView];
    
    [self.view addSubview:_rightScrollView];  
    
    [_rightScrollView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.equalTo(self.leftTableView.mas_right);
        make.top.bottom.right.equalTo(self.view);
    }];
    
    [_rightContentView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.edges.height.equalTo(self.rightScrollView);
    }];
    
    [_leftTableView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.left.bottom.equalTo(self.view);
        make.width.mas_equalTo(160);
    }];
    
    [_rightTableView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.top.bottom.height.equalTo(self.rightContentView);
        make.width.mas_equalTo(960);
    }];
    
    [_rightContentView mas_updateConstraints:^(MASConstraintMaker *make) {
        make.right.equalTo(self.rightTableView);
    }];
