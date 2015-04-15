ios-macros
==========
My collection of useful macros for iOS. These codes should be added to ...-Prefix.pch file. 

      //Colours
      #define rgba(r,g,b,a) [UIColor colorWithRed:r/255.0 green:g/255.0 blue:b/255.0 alpha:a/255.0]
      #define rgb(r,g,b) rgba(r,g,b,255)
      #define hex(val) [UIColor colorWithRed:((float)((val&0xFF0000)>>16))/255.0 green:((float)((val&0xFF00)>>8))/255.0 blue:((float)(val&0xFF))/255.0 alpha:1]
      #define bw(w,a) [UIColor colorWithWhite:w alpha:a]
      #define cgc(c) [c CGColor]
      
      //Primitive objects
      #define rect(x,y,w,h) CGRectMake(x,y,w,h)
      #define point(x,y)    CGPointMake(x,y)
      #define size(w,h)     CGSizeMake(w,h)
      #define range(s,l)    NSMakeRange(s,l)
      
      //Device Information
      #define uid [[[UIDevice currentDevice] identifierForVendor] UUIDString]
      #define isIPad   (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad)
      #define isIPhone (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPhone)
      #define isWidescreen (fabs((double)[[UIScreen mainScreen]bounds].size.height-(double)568)<DBL_EPSILON)
      #define isIPhone5 (isIPhone && isWidescreen)
      #define screen   [[UIScreen mainScreen] bounds].size
      
      //Threading
      #define runOnMainThread if (![NSThread isMainThread]) { dispatch_sync(dispatch_get_main_queue(), ^{ [self performSelector:_cmd]; }); return; };
      #define after(t,b) dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(t * NSEC_PER_SEC)), dispatch_get_main_queue(), b);
      
      //String Formatting
      #define f(base,...) [NSString stringWithFormat:base,##__VA_ARGS__]
      #define r(base,in,out) [base stringByReplacingOccurrencesOfString:in withString:out]
      #define ra(base,rpl,range) [base replaceCharactersInRange:range withAttributedString:rpl]
      
      //User defaults manipulation
      #define UDSet(k,o)     [[NSUserDefaults standardUserDefaults] setObject:o forKey:k]
      #define UDGet(k)       [[NSUserDefaults standardUserDefaults] objectForKey:k]
      #define UDSetBool(k,d) [[NSUserDefaults standardUserDefaults] setBoolean:d forKey:k]
      #define UDGetBool(k)   [[NSUserDefaults standardUserDefaults] booleanForKey:k]
      #define UDSetInt(k,d)  [[NSUserDefaults standardUserDefaults] setInteger:d forKey:k]
      #define UDGetInt(k)    [[NSUserDefaults standardUserDefaults] integerForKey:k]
      #define UDSync()       [[NSUserDefaults standardUserDefaults] synchronize]
      
      //Notification Center Management
      #define NCAdd(n,s)      [[NSNotificationCenter defaultCenter] addObserver:self selector:s name:n object:nil]
      #define NCRemove()      [[NSNotificationCenter defaultCenter] removeObserver:self]
      #define NCNotify(n,o)   [[NSNotificationCenter defaultCenter] postNotificationName:n object:o]
      
      //Fonts
      #define font(t,s) [UIFont fontWithName:t size:s]
      
      //Timer
      #define TStart(p,sel) [NSTimer scheduledTimerWithTimeInterval:p target:self selector:sel userInfo:nil repeats:YES]
      #define TStop(t) [t invalidate]
      
      //Alerts
      #define alert(t,m,c,...) [[[UIAlertView alloc] initWithTitle:t message:m delegate:nil cancelButtonTitle:c otherButtonTitles:##__VA_ARGS__,nil] show]
      #define alertD(t,m,c,...) [[[UIAlertView alloc] initWithTitle:t message:m delegate:self cancelButtonTitle:c otherButtonTitles:##__VA_ARGS__,nil] show]
