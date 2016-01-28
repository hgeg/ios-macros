ios-macros
==========
My collection of useful macros for iOS. These codes should be added to ...-Prefix.pch file. 

      //Colours
      #define rgba(r,g,b,a) [UIColor colorWithRed:r/255.0 green:g/255.0 blue:b/255.0 alpha:a/255.0]
      #define rgb(r,g,b) rgba(r,g,b,255)
      #define hex(val) [UIColor colorWithRed:((float)((val&0xFF0000)>>16))/255.0 green:((float)((val&0xFF00)>>8))/255.0 blue:((float)(val&0xFF))/255.0 alpha:1]
      #define bw(w,a) [UIColor colorWithWhite:w alpha:a]
      #define cgc(c) [c CGColor]
      #define black bw(0,1)
      #define white bw(1,1)
      #define transparent bw(0,0)
      
      //Primitive objects
      #define rect(x,y,w,h) CGRectMake(x,y,w,h)
      #define point(x,y)    CGPointMake(x,y)
      #define skewp(p)      CGPointMake(p.y,p.x)
      #define size(w,h)     CGSizeMake(w,h)
      #define range(s,l)    NSMakeRange(s,l)
      
      #define withRect(r,x,y,w,h) rect(r.origin.x+x, r.origin.y+y, r.size.width+w, r.size.height+h)
      #define withSize(s,w,h)     size(s.width+w,s.height+h)
      
      //Geometry
      #define xpos(v)       v.frame.origin.x
      #define ypos(v)       v.frame.origin.y
      #define center(v)     point(xpos(v)+width(v)/2,ypos(v)+height(v)/2)
      #define origin(v)     v.frame.origin
      #define width(v)      v.frame.size.width
      #define height(v)     v.frame.size.height
      #define inside(v,p)   (p.x>=xpos(v) and p.x<=xpos(v)+width(v)) and (p.y>=ypos(v) and p.y<=ypos(v)+height(v))
      
      //Device Information
      #define uid [[[UIDevice currentDevice] identifierForVendor] UUIDString]
      #define isIPad   (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad)
      #define isIPhone (UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPhone)
      #define isIPhone4 (fabs((double)[[UIScreen mainScreen]bounds].size.height-(double)480)<DBL_EPSILON)
      #define isIphone5 (fabs((double)[[UIScreen mainScreen]bounds].size.height-(double)568)<DBL_EPSILON)
      #define isIPhone6 (fabs((double)[[UIScreen mainScreen]bounds].size.height-(double)667)<DBL_EPSILON)
      #define isIPhone6p (fabs((double)[[UIScreen mainScreen]bounds].size.height-(double)736)<DBL_EPSILON)
      #define screen   [[UIScreen mainScreen] bounds].size
      
      //Threading
      #define runOnMainThread if (![NSThread isMainThread]) { dispatch_sync(dispatch_get_main_queue(), ^{ [self performSelector:_cmd]; }); return; };
      #define after(t,b) dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(t * NSEC_PER_SEC)), dispatch_get_main_queue(), b);
      #define async(b) dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), b);
      
      //String Operations
      #define format(base,...) [NSString stringWithFormat:base,##__VA_ARGS__]
      #define replace(base,in,out) [base stringByReplacingOccurrencesOfString:in withString:out]
      #define remap(base,rpl,range) [base replaceCharactersInRange:range withAttributedString:rpl]
      #define split(base,del) [base componentsSeparatedByString:del]
      #define charAt(base,index) [[base substringFromIndex:index] substringToIndex:1]
      
      //User defaults manipulation
      #define UDSet(k,o)     [[NSUserDefaults standardUserDefaults] setObject:o forKey:k]
      #define UDGet(k)       [[NSUserDefaults standardUserDefaults] objectForKey:k]
      #define UDSetBool(k,d) [[NSUserDefaults standardUserDefaults] setBool:d forKey:k]
      #define UDGetBool(k)   [[NSUserDefaults standardUserDefaults] boolForKey:k]
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
      #define alert(t,m,c,...) [[[UIAlertView alloc] initWithTitle:t message:m delegate:nil cancelButtonTitle:c otherButtonTitles:nil] show]
      #define alertD(t,m,c,...) [[[UIAlertView alloc] initWithTitle:t message:m delegate:self cancelButtonTitle:c otherButtonTitles:##__VA_ARGS__,nil] show]
      
      //Boolean Operators
      #define and &&
      #define or ||
