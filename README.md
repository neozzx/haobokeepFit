# haobokeepFit

Haobo is a company dedicated to fitness content.
This app mainly provides the following services for fitness enthusiasts:
-Professional fitness video
-Professional training program
-Professional healthy recipes
With it in hand, fitness has no trouble.

code:
	UICollectionView *collectionView = [[UICollectionView alloc] initWithFrame:CGRectMake(15, 0, SCREEN_W-30, SCREEN_H-64 - 49) collectionViewLayout:flowLayout];
	
	collectionView.bounces = YES;
	collectionView.pagingEnabled = YES;
	collectionView.showsHorizontalScrollIndicator = NO;
	collectionView.delegate = self;
	if ([[UIDevice currentDevice].systemVersion floatValue] >= 10) {
		collectionView.prefetchingEnabled = NO;
	}
	collectionView.dataSource = self;
	collectionView.backgroundColor = [UIColor clearColor];
	[self.view addSubview:collectionView];
	//    [collectionView registerClass:[UICollectionViewCell class] forCellWithReuseIdentifier:reuseID];
	[collectionView registerNib:[UINib nibWithNibName:NSStringFromClass([ZZZHomeInfoCollectionViewCell class]) bundle:nil] forCellWithReuseIdentifier:reuseID];
	self.collectionV = collectionView;
	self.collectionV.showsVerticalScrollIndicator = NO;
	[self.collectionV registerNib:[UINib nibWithNibName:NSStringFromClass([ZZZHomeHeaderableView class]) bundle:nil] forSupplementaryViewOfKind:UICollectionElementKindSectionHeader withReuseIdentifier:reuseIdentifierHeader];
  
  #pragma mark    -   UICollectionViewDelegate
- (void)scrollViewDidScroll:(UIScrollView *)scrollView {
    UIButton *firstBtn = self.btnContentView.subviews.firstObject;
    CGFloat index = scrollView.contentOffset.x / SCREEN_W;
    
    CGFloat changeW = index * firstBtn.width;
    NSInteger currentTag = index + .5;
    
    if (currentTag != self.selectBtn.tag) {
        
        self.selectBtn = self.btnContentView.subviews[currentTag];
    }
    
    self.indicatorView.centerX = firstBtn.centerX + changeW;
}
#pragma mark    -   ASJFriendTypeViewControllerDelegate

-(void)ZZZHealthyTypeViewController:(ZZZHealthyTypeViewController *)vc didScrollviewWithContentoffsetY:(CGFloat)offsetY
{
    self.preOffsetY = offsetY;
    if (offsetY > 0) {
        self.headerView.y = - vc.topH;
//        self.headerView.y = - offsetY;

    } else {
        self.headerView.y = - offsetY - vc.topH;
    }
}
  
