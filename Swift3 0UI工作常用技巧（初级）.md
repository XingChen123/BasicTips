#Swift3.0UI工作常用技巧(初级^_^)
######by 变态杀人小番茄

##1 目录
###<font color=#ff6347 >1 文字篇</font>
* [1.1［TextField］如何给Textfield里面添加Logo](#w1)
* [1.2［Label］一句话中文字设置不同颜色](#w2)
* [1.3 [TabBar]修改tabbar图片颜色](#w3)
* [1.4 [TabBar]按tabbar时候给其添加方法](#w4)
* [1.5 [Alert]AlertController](#w5)
* [1.6 [<font color=FF8C00 >Label</font>]如何get到label的长和宽](#w6)
* [1.1如何给Textfield里面添加Logo](#TextField1)

###<font color=#ff6347 >2 第三方软件应用篇</font>
* [2.1［抽屉控件］添加MMDrawerContoller方法](#T1)




－－－－－－－－－－－－－－－－－－－－－－－－－－

##<font color=#ff6347 >1 文字篇</font>
####<a name = "w1"></a>1.1如何给Textfield里面添加Logo

     passwordImgView = UIImageView(image: UIImage(named: "passwordImg"))
     passwordImgView.frame = CGRect(x: 0, y: 0, width: 25, height: 25)
     passWordTF.leftViewMode = .always
     passWordTF.leftView = passwordImgView

####<a name = "w2"></a>1.2一句话中文字设置不同颜色

     signUpLB1 = UILabel(frame: CGRect(x: 0, y: 0, width: 0, height: 0))
     let myMutableString = NSMutableAttributedString(string: "Don't have an account?SIGN UP", attributes: [NSForegroundColorAttributeName : UIColor.white])
     //注释： 从第22个字节开始，共长7个字节是绿色的
     myMutableString.addAttribute(NSForegroundColorAttributeName, value: UIColor.green, range: NSRange(location: 22, length: 7))
     signUpLB1.attributedText = myMutableString

####<a name = "w3"></a>1.3 修改tabbar图片颜色
	//注释： 第一行设置被选择时的图片，第二行设置被选择时图片颜色
 	navNavigationPage2.tabBarItem.selectedImage = UIImage(named: "calendarbar_b")
  	self.tabBar.tintColor = defaultGreen
####<a name = "w4"></a>1.4 按tabbar时候给其添加方法（直接用tabbardelegate就可以了）
	override func tabBar(_ tabBar: UITabBar, didSelect item: UITabBarItem) {
    }
####<a name = "w5"></a>1.5 AlertController的使用
平时占位用的弹出alert：
			
		let alertController = UIAlertController(title: "", message: "", preferredStyle: UIAlertControllerStyle.alert)
        let yes = UIAlertAction(title: "OK", style: .default, handler: { (action) -> Void in
            
        })
        alertController.addAction(yes)
        present(alertController, animated: true, completion: nil)


actionsheet一样的alert：


		let alertController = UIAlertController()
        let holiday = UIAlertAction(title: "New Holiday", style: .default, handler: { (action) -> Void in
            let centerViewController = NewHolidayViewController()
            drawerController0.centerViewController = centerViewController
        })
        let cancel = UIAlertAction(title: "Cancel", style: .cancel, handler: { (action) -> Void in
            
        })
        
        alertController.addAction(holiday)
        alertController.addAction(cancel)
        present(alertController, animated: true, completion: nil)
        


####<a name = "w6"></a>1.6 如何get到label的长和宽
先在Utils中写一个可以get长宽的类，CGSize型

    class func getStringWidth( str: String , font : UIFont) -> CGSize {
        var sizeOfString = CGSize()
        let finalDate = str
        let fontAttributes = [NSFontAttributeName: font] // it says name, but a UIFont works
        sizeOfString = (finalDate as NSString).sizeWithAttributes(fontAttributes)
        
        return sizeOfString
    }
调用这个类的方法 【例子】

	let skillButtonLength1 = KKUtils.getStringWidth((skillButtons[1].titleLabel?.text)!, font: (skillButtons[1].titleLabel?.font)!)
    if  skillButtonLength1.width >= lengthOfButtonLB {
    skillButtons[1].titleLabel?.numberOfLines = 2
                }






## <font color=#ff6347 >2 第三方软件应用篇 </font>
####<a name = "T1"></a>2.1添加MMDrawerContoller方法
参考资料：http://www.jianshu.com/p/1064dc5ee65e

&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; http://www.jianshu.com/p/d08503869cf2

&nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;http://www.cocoachina.com/swift/20150630/12305.html

**<font color=#228b22 size = 3>＊＊Step1: 先安装Pod＊＊</font>**

打开项目创建空白页（Empty）写上pod 'MMDrawerController', '~> 0.5.7'，然后在终端里打开empty所在地方，输入 pod install

［注释：empty文件创建的位置有说法，好像在项目最外面］


**<font color=#228b22 size = 3>＊＊Step2: 创建头文件＊＊</font>**

创建一个HeaderFile文件名字叫<font color=#7cfc00>Bridging-Header</font>(名字可以随意),在这个文件中写

	#import<MMDrawerController/MMDrawerController.h>
	#import<MMDrawerController/MMDrawerController+Subclass.h>
	#import<MMDrawerController/UIViewController+MMDrawerController.h>
然后到项目设置－Build Setting-搜索框输入bridg -找到Swift Complier-Code Generation里的Objective-C bridging Header,把刚才<font color=#7cfc00>随意些的那个名字</font>复制到这里来

**<font color=#228b22 size = 3>＊＊Step3: 引用代码＊＊</font>**

引用代码，初始化根视图，左视图，中心视图，右视图（在那儿写都行，不是非要在appdelegate里写）

		//这两行必须有，在每个文件的最最上面
		import  MMDrawerController
		public var drawerController0 : MMDrawerController!

 		//设置视图
        let leftMenuController = LeftHomeTutorViewController()
        let rightMenuController = FiltersViewController()
        let leftNavigationController = UINavigationController(rootViewController: leftMenuController)
        let rightNavigationController = UINavigationController(rootViewController: rightMenuController)
        let centerViewController = DashboardTutorTabBarController()
        //        let centerViewController = DashboardStudentTabBarController()
        let centerNavigationController = centerViewController
        
        
        drawerController0 = MMDrawerController(center: centerNavigationController, leftDrawerViewController: leftNavigationController, rightDrawerViewController: rightNavigationController)
        drawerController0.maximumLeftDrawerWidth = ScreenWidth * 0.8
        drawerController0.maximumRightDrawerWidth = ScreenWidth * 0.8
        //手势
        drawerController0.openDrawerGestureModeMask = MMOpenDrawerGestureMode.all
        drawerController0.closeDrawerGestureModeMask = MMCloseDrawerGestureMode.all
        
        
        //设置动画，这里是设置打开侧栏透明度从0到1
        drawerController0.setDrawerVisualStateBlock { (drawerController, drawerSide, percentVisible) -> Void in
            
            var sideDrawerViewController:UIViewController?
            if(drawerSide == MMDrawerSide.left){
                sideDrawerViewController = drawerController?.leftDrawerViewController;
            }else if(drawerSide == MMDrawerSide.right){
                sideDrawerViewController = drawerController?.leftDrawerViewController;
            }
            sideDrawerViewController?.view.alpha = percentVisible
        }
        
        self.present(drawerController0, animated: false , completion: nil)
        

**<font color=#228b22 size = 3>＊＊Step4：使用时的一些跳页技巧＊＊</font>**


改变中心页面： 			

      drawerController0.centerViewController = DashboardTutorTabBarController()
      
跳转以后是拉开抽屉的状态：

     	let centerNavigationController = DashboardTutorTabBarController()
        let leftViewController = LeftHomeTutorViewController()
        let leftNavigationController = UINavigationController(rootViewController: leftViewController)
        //let appDelegate = UIApplication.shared.delegate as! AppDelegate
        //appDelegate.drawerController.centerViewController = centerNavigationController
        drawerController0.centerViewController = centerNavigationController
        drawerController0.leftDrawerViewController = leftNavigationController
        //这里表示拉开状态
        drawerController0.toggle(MMDrawerSide.left, animated: true, completion: nil)





