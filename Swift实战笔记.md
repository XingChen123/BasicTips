#Swift实战总结   
######by 变态杀人小番茄
self.view.layer.zposition = 1


    func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
    self.window = UIWindow(frame: UIScreen.mainScreen().bounds)

    var storyboard = UIStoryboard(name: "Main", bundle: nil)

    var initialViewController = storyboard.instantiateViewControllerWithIdentifier("LoginSignupVC") as! UIViewController

    self.window?.rootViewController = initialViewController
    self.window?.makeKeyAndVisible()

    return true
}
## 1目录

###1.2第二章_创建小件篇
* [2.1创建图片Image](#创建图片)
* [2.2创建文本框Textfield](#创建文本框)
* [2.3创建按钮Button](#创建按钮)
* [2.4创建Label](#创建Label)
* [2.5创建switch](#2.5创建switch)
* [2.6创建slide](#2.6创建slide)

###1.3第三章_创建各种View
* [3.1创建ScrollView和pageControl](#3.1创建ScrollView)
* [3.2创建TableView](#3.2创建TableView)
* [3.2创建创建Navigation](#3.2创建创建Navigation)

###1.4第四章_创建各种组件
* [4.1UIActionSheetDelegate](#4.1UIActionSheetDelegate)
* [4.2UIImagePickerControllerDelegate](#4.2UIImagePickerControllerDelegate)


###1.5第五章_加入第三方库
* [5.1安装pod的方法](#5.1安装pod的方法)

##第二章 创建小件篇
###<a name = "创建图片"></a>2.1创建图片的方法

    let imageName : String = "Image1"
    let image = UIImage(named : imageName)
    let imageView = UIImageView(image : image!)
    addSubview(imageView)
    //图片圆角
    vImg.layer.cornerRadius = 8;
    vImg.layer.masksToBounds = true;


###<a name = "创建文本框"></a>2.2创建文本框的方法

    let userTF = UITextField(frame:CGFloat(0,0,0,0))
    addSubview(userTF)
   >TextField属性
    
    userTF.placeholder = "预设文字输入处"
    MimaTF.secureTextEntry = true
    userTF.font = UIFont.systemFontofSize(20)
    userTF.borderStyle = UTextBorderStyle.RoundedRect
    userTF.autocorrectionType = UITextAutocorrectionType.No
    userTF.keyboardType = UIKeyboardType.Default
    userTF.returnKeyType = UIReturnKeyType.Done
    userTF.clearButtonMode = UITextFieldViewMode.whileEditing
    userTF.contentVerticalAlignment = UIControlContentVerticaAlignment.Centre
    //————————————设置输入结束后键盘弹回
    func textFieldShouldReturn(textField: UITextField) -> Bool {
        self.endEditing(true)
        return false
    }
   

###<a name = "创建按钮"></a>2.3创建按钮的方法

    let pButton = UIButton(type : UIButtonType.System) as UIButton
    给button添加事件
    textButton.addTarget(self,action:“buttonActions:”,forControlEvents:UIControlEvents.TouchUpInside)
    func buttonActions(sender: UIButton!) {
        println(“tapped button”)
    }
    addSubview(pButton)
   >Button属性 
    
    pButton.setTitle("xxx",forState : UIControlState.Normal)
    pButton.backgroundColor = UIColor.whiteColor
    pButton.setTitleColor(UIColor(red:152/255,green:152/255,blue:152/255,alpha:1.0),forState:UIControlState.Normal)


###<a name = "创建Label"></a>2.4创建Label的方法

    var label = UILabel(frame: CGRectMake(0, 0, 200, 21))
    label.center = CGPointMake(160, 284)
    label.textAlignment = NSTextAlignment.Center
    label.text = "I'am a test label"
    self.view.addSubview(label)
    label1.font = UIFont.systemFontOfSize(25)

###<a name = "2.5创建switch"></a>2.5创建switch

    let switch2=UISwitch(frame:CGRectMake(150, 300, 0, 0));
    switch2.on = false
        switch2.onTintColor = UIColor(red: 0/255, green: 51/255, blue: 102/255, alpha: 1.0)
        switch2.setOn(true, animated: false);
        switch2.addTarget(self, action: "switch2DidChange:", forControlEvents: .ValueChanged);
        self.view.addSubview(switch2);
>使用switch

     func switch2DidChange(sender:UISwitch) {
        let setting = sender.on
        switch2.setOn(setting, animated: true)
    }

###<a name = "2.6创建slide"></a>2.6创建slide

    let slider1 = UISlider(frame:CGRectMake(0, 0, 0, 0))
    slider1.minimumValue = 0
        slider1.maximumValue = 100
        slider1.continuous = true
        slider1.tintColor = UIColor.blueColor()
        slider1.value = 50
        slider1.addTarget(self, action: "slider1DidChange:", forControlEvents: .ValueChanged)
        self.view.addSubview(slider1)
        
>使用slide
    
    func slider1DidChange(sender:UISlider) {
        let slider1number = lroundf(sender.value)
        labelslider1.text = "\(slider1number)"
    }


##第三章 创建各种View篇


###<a name = "3.1创建ScrollView"></a>3.1创建ScrollView和pageControl `UIScrollViewDelegate`



   		let scrollview = UIScrollView(frame: UIScreen.mainScreen().bounds)
   	 	var image1 = UIImage(named: "1")
    	var image2 = UIImage(named: "2")
    	var image3 = UIImage(named: "3")
    	var curpage: Int = 1 
    	var pageControl : UIPageControl = UIPageControl(frame: CGRectMake(150,400,100,30))
  
    override func viewDidLoad() {
       super.viewDidLoad()
    
        var imageView1 = UIImageView(image: image1!)
        var imageView2 = UIImageView(image: image2!)
        var imageView3 = UIImageView(image: image3!)
        
        self.view.addSubview(imageView3)
        self.view.addSubview(imageView2)
        self.view.addSubview(imageView1)
        
        scrollview.addSubview(imageView1)
        scrollview.addSubview(imageView2)
        scrollview.addSubview(imageView3)
        
        let width:CGFloat = view.frame.size.width
        let height: CGFloat = view.frame.size.height * 0.64
        
        scrollview.frame = CGRectMake(0, 0, width, height )
        
        imageView1.frame  = CGRectMake(width, 0, width, height )
        imageView2.frame = CGRectMake(2*width, 0, width, height)
        imageView3.frame = CGRectMake(0, 0, width, height)
        
        
        scrollview.contentSize = CGSize(width: width*3 ,height: height)
        scrollview.contentOffset = CGPointMake(width, 0)
        
        scrollview.delegate = self
        scrollview.bounces = false
        scrollview.pagingEnabled = true
        scrollview.showsHorizontalScrollIndicator = false
        scrollview.showsVerticalScrollIndicator = false
        view.addSubview(scrollview)
        
        //设置pagecontrol的方法见下////////////////////////
        configurePageControl()
        
    }
    
>设置scrollview的方法
    
    func scrollViewDidEndDecelerating(scrollView: UIScrollView) {
        let pageNumber = round(scrollview.contentOffset.x / scrollview.frame.size.width)
        pageControl.currentPage = Int(pageNumber)
    }
    
    
>设置pagecontrol的方法
    
    func configurePageControl(){
        self.pageControl.numberOfPages = 3
        self.pageControl.currentPage = 1
        self.pageControl.tintColor = UIColor.blackColor()
        self.pageControl.pageIndicatorTintColor = UIColor.whiteColor()
        self.pageControl.currentPageIndicatorTintColor = UIColor(red: 255/255, green: 153/255, blue: 163/255, alpha: 1.0)
        self.view.addSubview(pageControl)
    }

###<a name = "3.2创建TableView"></a>3.2创建TableView

> 创建成组的TableView（类似微信ME）
    
		var nameArray : Dictionary<Int, [String]>?
		var imageArray : Dictionary<Int, [String]>?
 		var headers:[String]?
 		
 	override func viewDidLoad() {
        super.viewDidLoad()
        
        self.nameArray =  [
            0:[String]([
                "变态杀人小星星"]),
            1:[String]([
                "相册",
                "收藏",
                "钱包"]),
            2:[String]([
                "表情"]),
            3:[String]([
                "设置"])
        ]
        
        
        
        self.imageArray =  [
            0:[String]([
                "头像"]),
            1:[String]([
                "相册",
                "收藏",
                "钱包"]),
            2:[String]([
                "表情"]),
            3:[String]([
                "设置"])
        ]
        
        self.headers = ["aa","bb"]
        
    }
    
>如果是在UIView中添加TableView需要加UITableViewDelegate和UITableViewDataSource

    	//并在viewdidload（）中添加如下
    	self.tableView = UITableView(frame:self.view.frame, style:UITableViewStyle.Grouped)
        self.tableView!.delegate = self
        self.tableView!.dataSource = self
        //创建一个重用的单元格
        self.tableView!.registerClass(UITableViewCell.self, forCellReuseIdentifier: "SwiftCell")
        self.view.addSubview(self.tableView!)

>TableView的几个属性

    
    //有4个分区
    func numberOfSectionsInTableView(tableView: UITableView) -> Int {
        return 4;
    }
 
	//表格行数（每个分区中的行数）
    func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        let data = self.nameArray?[section]
        return data!.count
    }
    
    //每个分区的header的名字
    func tableView(tableView: UITableView, titleForHeaderInSection section: Int) -> String? {
            var headers =  self.headers!;
            return headers[section];
        }
    func tableView(tableView:UITableView, titleForFooterInSection
        section:Int)->String?
    {
        //        let data = self.allnames?[section]
        //        return "有\(data!.count)个控件"
        return ""
    }
    
    
    //设置cell中的内容
    func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath)
        -> UITableViewCell
    {
        //为了提供表格显示性能，已创建完成的单元需重复使用
        let identify:String = "SwiftCell"
        //同一形式的单元格重复使用，在声明时已注册
        let cell = tableView.dequeueReusableCellWithIdentifier(identify, forIndexPath: indexPath)
            as UITableViewCell
        cell.accessoryType = UITableViewCellAccessoryType.DisclosureIndicator
        
        let secno = indexPath.section
        var data = self.allnames?[secno]
        var data2 = self.imageArray?[secno]
        cell.textLabel?.text = data![indexPath.row]
        cell.imageView?.image = UIImage(named: data2![indexPath.row])
        //        cell.imageView?.layer.cornerRadius = 50
        if (indexPath.section == 0 ){
           if (indexPath.row == 0) {
           
           }else {
           
           }

        } else if (indexPath.section == 1) {
        
        }
        
        return cell
    }
    
    
    //每个header的高度
    func tableView(tableView: UITableView, heightForHeaderInSection section: Int) -> CGFloat {
        if (section == 0 ) {
            //            return (self.tableView?.frame.height)! * 0.1
            return 65
        } else {
            return (self.tableView?.frame.height)! * 0.012
        }
    }
    
    
    
    // 选择cell以后的动作（UITableViewDelegate 方法，处理列表项的选中事件）
    func tableView(tableView: UITableView, didSelectRowAtIndexPath indexPath: NSIndexPath)
    {
        self.tableView!.deselectRowAtIndexPath(indexPath, animated: true)
        
        let itemString = self.allnames![indexPath.section]![indexPath.row]
        
        if indexPath.section == 0 {
            
            let secondViewController : GeRenZiLiao1_1 = GeRenZiLiao1_1()
		// let rootView: Me1 = Me1()
		// let navigation = UINavigationController(rootViewController:secondViewController)
		// self.navigationController?.pushViewController(navigation, animated: true)
            self.presentViewController(secondViewController, animated: true, completion: nil)
            
        }else if indexPath.section == 1 {
            
            if indexPath.row == 0 {
               self.presentViewController(Find(), animated: true, completion: nil)
            }
            
        }else {
        
        let alertview = UIAlertView();
        alertview.title = "提示!"
        alertview.message = "你选中了【\(itemString)】";
        alertview.addButtonWithTitle("确定")
        alertview.show();
    
        }
        
     }
    
###<a name = "创建Navigation"></a>创建Navigation的方法
>NavigationBar

 		let navigationBar = UINavigationBar(frame: CGRectMake(0,0,self.view.frame.size.width,60))
        navigationBar.backgroundColor = UIColor.blackColor()
        navigationBar.delegate = self
        let navigationItem = UINavigationItem()
        navigationItem.title = "XXX"
        navigationBar.barStyle = UIBarStyle.Black
        navigationBar.tintColor = UIColor.whiteColor()
        navigationBar.titleTextAttributes = [NSForegroundColorAttributeName:UIColor.whiteColor()]
        navigationBar.items = [navigationItem]
        self.view.addSubview(navigationBar)


##第四章 创建各种组件篇


###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate

	func RightBtn_clicked(sender:UIButton!){
        print("rightbutton clicked")
        let myActionSheet = UIActionSheet()
        myActionSheet.delegate = self
        myActionSheet.addButtonWithTitle("拍照")
        myActionSheet.addButtonWithTitle("从手机相册选择")
        myActionSheet.addButtonWithTitle("保存图片")
        myActionSheet.addButtonWithTitle("取消")
        myActionSheet.cancelButtonIndex = 3
        myActionSheet.showInView(self.view)
    }
    
      func actionSheet(actionSheet: UIActionSheet, clickedButtonAtIndex buttonIndex: Int) {
        if(buttonIndex == 0) {
            let imageFromSource = UIImagePickerController()
            imageFromSource.delegate = self
            imageFromSource.allowsEditing = false
            if UIImagePickerController.isSourceTypeAvailable(UIImagePickerControllerSourceType.Camera) {
                imageFromSource.sourceType = UIImagePickerControllerSourceType.Camera
            }else {
                var alertView = UIAlertView()
                alertView.addButtonWithTitle("OK")
                alertView.title = "Alert"
                alertView.message = "无法连接相机，请尝试从相册选取”"
                alertView.show()
                
            }
            self.presentViewController(imageFromSource, animated: true, completion: nil)

        }else if (buttonIndex == 1) {
            let imageFromSource = UIImagePickerController()
            imageFromSource.delegate = self
            imageFromSource.allowsEditing = false

            if UIImagePickerController.isSourceTypeAvailable(UIImagePickerControllerSourceType.PhotoLibrary) {
                imageFromSource.sourceType = UIImagePickerControllerSourceType.PhotoLibrary
            
            }else {
                let alertView = UIAlertView()
                alertView.addButtonWithTitle("OK")
                alertView.title = "Alert"
                alertView.message = "无法连接相册"
                alertView.show()
                
            }
            self.presentViewController(imageFromSource, animated: true, completion: nil)
            
            
        }else if (buttonIndex == 2) {
            
        }else {
            
        }
    }

###<a name = "4.2UIImagePickerControllerDelegate"></a>4.2UIImagePickerControllerDelegate
`还有一些有关ImagePicker使用照相机的内容在4.1中`

 	func imagePickerController(picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : AnyObject]) {
        let temp: UIImage = info[UIImagePickerControllerOriginalImage] as! UIImage
        let tempView = UIImageView(image: temp)
     
        let ImageView1 = UIImageView(image: temp)
        ImageView1.frame = CGRectMake(0,CGFloat((self.view.frame.size.height - self.view.frame.size.width) * 0.5),self.view.frame.size.width,self.view.frame.size.width)
        self.view.addSubview(ImageView1)
        
        self.dismissViewControllerAnimated(true, completion: {})
        
        self.presentViewController(GeRenZiLiao1_1(), animated: true, completion: nil)
        
        let ImageView2 = ImageView1
        let Image1 = temp
        
    }
    
    
##第五章 安装第三方库

###<a name = "5.1安装pod的方法"></a>5.1安装pod的方法


###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
v

###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
###<a name = "4.1UIActionSheetDelegate"></a>4.1UIActionSheetDelegate
