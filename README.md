
# 9 - Middleware GetX
 
### الفكرة الرئيسية هي تطبيق الصلاحيات في التطبيق .. مثلا في حال سجل المستخدم دخول قبل هيك هو مش بحاجة يسجل مرة أخرى 


// step 1 

       initialRoute: "/",
        getPages: [
         GetPage(
           name: "/",
           page: () => const Login(),
         ),
         GetPage(name: "/Home", page: () => Home()),
       ],

// step 2 

          // in login Screen
          onPressed: () {
            sharepref!.setString("id", "1");
            Get.offNamed("home");
          },
          
          
          
          // in home Scereen
          onPressed: () {
            sharepref!.clear();
            Get.offAllNamed("/");
          },
          
          
 // step  3
 
       class AuthMiddleWare extends GetMiddleware {
        @override
        RouteSettings? redirect(String? route) {
           if (sharepref!.getString("id") != null) {
               return const RouteSettings(
               name: "/home",
            );
          }
        }

// step 4 

        GetPage(
          name: "/",
          page: () => const Login(),
          middlewares: [AuthMiddleWare()],
        ),
 
 
### أخر خطوة احنا ضفنا middlewares الي راح يروح الها بالاول ويفحص ال Route













 
 
