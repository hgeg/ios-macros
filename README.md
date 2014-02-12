ios-macros
==========
My collection of useful macros for iOS. These codes should be added to ...-Prefix.pch file. 

      //Colours
      #define rgba(r,g,b,a) [UIColor colorWithRed:r/255.0 green:g/255.0 blue:b/255.0 alpha:a/255.0]
      #define rgb(r,g,b) [UIColor colorWithRed:r/255.0 green:g/255.0 blue:b/255.0 alpha:1]
      #define hex(val) [UIColor colorWithRed:((float)((val&0xFF0000)>>16))/255.0 green:((float)((val&0xFF00)>>8))/255.0 blue:((float)(val&0xFF))/255.0 alpha:1]
      #define white [UIColor whiteColor]
      
      //Device Information
      #define uid [[[UIDevice currentDevice] identifierForVendor] UUIDString]
      #define isIPad   (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad)
      #define isIPhone (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPhone)
      #define isWidescreen (fabs((double)[[UIScreen mainScreen]bounds].size.height-(double)568)<DBL_EPSILON)
      #define isIPhone5 (isIPhone && isWidescreen)
      
      //Threading
      #define runOnMainThread if (![NSThread isMainThread]) { dispatch_sync(dispatch_get_main_queue(), ^{ [self performSelector:_cmd]; }); return; };
      
      //String Formatting
      #define fmt(base,...) [NSString stringWithFormat:base,##__VA_ARGS__]
      
      //User defaults manipulation
      #define UD_setObj(key,obj) [[NSUserDefaults standardUserDefaults] setObject:obj forKey:key]
      #define UD_getObj(key)     [[NSUserDefaults standardUserDefaults] objectForKey:key] ? [[NSUserDefaults standardUserDefaults] objectForKey:key] : @"_HGNone"
      #define UD_setBool(key,d)  [[NSUserDefaults standardUserDefaults] setBool:d forKey:key]
      #define UD_getBool(key)    [[NSUserDefaults standardUserDefaults] boolForKey:key] ? [[NSUserDefaults standardUserDefaults] boolForKey:key] : false
      #define UD_setInt(key,d)   [[NSUserDefaults standardUserDefaults] setInteger:d forKey:key]
      #define UD_getInt(key)     [[NSUserDefaults standardUserDefaults] integerForKey:key] ? [[NSUserDefaults standardUserDefaults] integerForKey:key] : 0
      #define UD_sync()   [[NSUserDefaults standardUserDefaults] synchronize]
      
      //Notification Center Management
      #define NC_addObserver(n,sel) [[NSNotificationCenter defaultCenter] addObserver:self selector:sel name:n object:nil]
      #define NC_removeObserver() [[NSNotificationCenter defaultCenter] removeObserver:self]
      #define NC_postNotification(n,obj) [[NSNotificationCenter defaultCenter] postNotificationName:n object:obj]
      
      //Fonts
      #define font(t,s) [UIFont fontWithName:t size:s]
      
      //Timer
      #define startTimer(p,sel) [NSTimer scheduledTimerWithTimeInterval:p target:self selector:sel userInfo:nil repeats:YES]
      #define stopTimer(t) [t invalidate]
      
      //Alerts
      #define alert(t,m,c,...) [[[UIAlertView alloc] initWithTitle:t message:m delegate:nil cancelButtonTitle:c otherButtonTitles:##__VA_ARGS__,nil] show]
      #define alertD(t,m,c,...) [[[UIAlertView alloc] initWithTitle:t message:m delegate:self cancelButtonTitle:c otherButtonTitles:##__VA_ARGS__,nil] show]
