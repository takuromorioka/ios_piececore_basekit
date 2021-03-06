### pieceライブラリBaseKitのインストール

Pieceの基本となる部品をライブラリにしました。  
Flyer、info、Shopping、Couponが利用可能です。  
フルパッケージよりも、ダウンロードが軽くなり、許可設定も少なくなります。

CocoaPodを使用してインストールして下さい。  
プロジェクト直下にpodfileを配置し、下記を記述します。  
pod 'PieceCoreBase', :git => 'https://github.com/jokerpiece/ios_piececore_basekit.git'

ターミナルからpod installをするとPieceに必要なモジュールがダウンロードされます。  
プロジェクト.xcworkspaceを開き開発を行って下さい。

### 利用方法
AppDelegeteにCoreDelegateを継承させます。
下記メソッドをオーバライドして、必要な情報を設定します。

| 名前               | 説明                                                                           |
| ---                | ---                                                                            |
| setConfig |API連携用のshopIdと、バージョンアップ判定用のappIdをセットします。|
| setThemeColor　|ナビゲーションやタブバーのテーマカラーを設定します。|
| getTabbarDataList |必要な機能(piece)を定義します。|

下記にAppDelegateの記述例を記します。  

AppDelegate.h  

    //AppDelegate.h

    #import <UIKit/UIKit.h>
    #import "CoreDelegate.h"

    @interface AppDelegate : CoreDelegate

    @property (strong, nonatomic) UIWindow *window;


    @end


AppDelegate.m

    //  pieceAppDelegate.m

    #import "AppDelegate.h"
    #import "FlyerViewController.h"
    #import "InfoListViewController.h"
    #import "CategoryViewController.h"
    #import "TabbarViewController.h"


    @implementation AppDelegate


    -(void)setConfig{
        [PieceCoreConfig setShopId:@"pieceSample"];
        [PieceCoreConfig setAppId:@""];
    }

    -(void)setThemeColor{
        self.theme = [[ThemeData alloc]initThemeCute];
    }

    - (NSMutableArray *)getTabbarDataList
    {
        NSMutableArray *tabbarDataList = [NSMutableArray array];
        FlyerViewController *flyerVc =[[FlyerViewController alloc] initWithNibName:@"FlyerViewController" bundle:nil];
    
    
        [tabbarDataList addObject:[[TabbarData alloc]initWithViewController:
                               [[FlyerViewController alloc] initWithNibName:@"FlyerViewController" bundle:nil]
                                                                tabTitle:@"Flyer"
                                                                  title:@"FLYER"]];
    
        [tabbarDataList addObject:[[TabbarData alloc]initWithViewController:
                               [[InfoListViewController alloc] initWithNibName:@"InfoListViewController" bundle:nil]
                                                                tabTitle:@"Info"
                                                                  title:@"INFO"]];
        [tabbarDataList addObject:[[TabbarData alloc]initWithViewController:
                               [[CategoryViewController alloc] initWithNibName:@"CategoryViewController" bundle:nil]
                                                                tabTitle:@"Shopping"
                                                                  title:@"SHOPPING"]];
        [tabbarDataList addObject:[[TabbarData alloc]initWithViewController:
                               [[CouponViewController alloc] initWithNibName:@"CouponViewController" bundle:nil]
                                                                tabTitle:@"Coupon"
                                                                  title:@"COUPON"]];

    
        return tabbarDataList;
    }

    @end

### 機能クラス
Pieceで提供している機能と紐づくクラス名は下記の通りです。  

| 名前               | 説明                                                                           |
| ---                | ---                                                                            |
| FlyerViewController |フライヤー|
| InfoListViewController　|お知らせ一覧|
| CategoryViewController |ショッピング|
| CouponViewController|クーポン|


### その他
- Build Settings > Enable BitcodeをNOにして下さい。  
- info.plistに以下を追記します。  
	 `<dict>`  
        `<key>NSAllowsArbitraryLoads</key>`  
        `<true/>`  
    `</dict>`