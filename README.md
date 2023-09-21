# checkPasswordStrong


## Image 
![Screenshot 2023-09-22 010252](https://github.com/SADIQ12ALOTMI/checkPasswordStrong/assets/78486332/c9207ec4-2bcd-4896-b0c9-c9c92c86b771)
## video
https://github.com/SADIQ12ALOTMI/checkPasswordStrong/assets/78486332/917309e3-7b07-4a73-9269-33ddd4c33f2c

## code full Flutter
``` dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: PasswordStrengthCheckerApp(),
    );
  }
}

class PasswordStrengthCheckerApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: PasswordStrengthCheckerScreen(),
    );
  }
}

class PasswordStrengthCheckerScreen extends StatefulWidget {
  @override
  _PasswordStrengthCheckerScreenState createState() =>
      _PasswordStrengthCheckerScreenState();
}

class _PasswordStrengthCheckerScreenState
    extends State<PasswordStrengthCheckerScreen> {
  String password = '';
  bool showPassword = false;

  int calculateStrength(String password) {
    int strength = 1;

    if (password.length > 6) {
      strength++;
    }

    if (password.length >= 10) {
      strength++;
    }

    if (RegExp(r'[A-Z]').hasMatch(password)) {
      strength++;
    }

    if (RegExp(r'[0-9]').hasMatch(password)) {
      strength++;
    }

    if (RegExp(r'[A-Za-z0-9]').hasMatch(password)) {
      strength++;
    }

    return strength;
  }

  void updateStrength() {
    int strength = calculateStrength(password);
    if (strength <= 3) {
      setState(() {
        containerState = 'Weak';
      });
    } else if (strength >= 3 && strength <= 5) {
      setState(() {
        containerState = 'Moderate';
      });
    } else {
      setState(() {
        containerState = 'Strong';
      });
    }
  }

  String containerState = 'Weak';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.black87,
      appBar: AppBar(
        title: Text('Password Strength Checker'),
      ),
      body: SizedBox(
        width: MediaQuery.sizeOf(context).width,
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
         crossAxisAlignment: CrossAxisAlignment.center,
         children: [
           SizedBox(
             width: 400,
             child: Column(
               children: [
                 Container(
                   width: 400,
                   decoration: BoxDecoration(
                     borderRadius: BorderRadius.only(
                       topLeft: Radius.circular(20),
                       topRight: Radius.circular(20),
                     ),
                     color: Colors.grey[800],
                     boxShadow: [
                       BoxShadow(
                         color: Colors.black.withOpacity(0.2), // Adjust the opacity as needed
                         blurRadius: 10.0, // Adjust the blur radius as needed
                         offset: Offset(0, 2), // Adjust the offset as needed
                       ),
                     ],
                   ),
                   padding: EdgeInsets.all(30),
                   child: Column(
                     mainAxisAlignment: MainAxisAlignment.center,
                     crossAxisAlignment: CrossAxisAlignment.center,
                     children: [
                       Text(
                         'Password Strength Checker',
                         style: TextStyle(
                           color: Colors.grey[600],
                           fontWeight: FontWeight.bold,
                           fontSize: 24,
                         ),
                       ),
                       SizedBox(height: 10),
                       Column(
                         crossAxisAlignment: CrossAxisAlignment.start,
                         children: [
                           Container(
                             width: double.infinity,
                             child: TextField(
                               onChanged: (value) {
                                 setState(() {
                                   password = value;
                                 });
                                 updateStrength();
                               },
                               obscureText: !showPassword,
                               style: TextStyle(color: Colors.white70,fontSize: 20,fontWeight: FontWeight.bold),
                               decoration: InputDecoration(
                                 hintText: 'Password',
                                 hintStyle: TextStyle(
                                   color: Colors.grey[600],
                                 ),
                                 filled: true,
                                 fillColor: Colors.grey[900],
                                 border: InputBorder.none,
                                 suffixIcon: GestureDetector(
                                   onTap: () {
                                     setState(() {
                                       showPassword = !showPassword;
                                     });
                                   },
                                   child: SizedBox(
                                     width: 70,
                                     height: 40,
                                     child: Card(
                                       color: Colors.grey[800],
                                       shape: RoundedRectangleBorder(
                                         borderRadius: BorderRadius.zero,
                                       ),
                                       child: Padding(
                                         padding: const EdgeInsets.all(8.0),
                                         child: Center(
                                           child: Text(
                                             showPassword ? 'HIDE' : 'SHOW',
                                             style: TextStyle(
                                               color: Colors.white70,
                                               fontSize: 12,
                                               letterSpacing: 0.15,
                                               textBaseline: TextBaseline.alphabetic,
                                             ),
                                           ),
                                         ),
                                       ),
                                     ),
                                   ),
                                 ),
                               ),
                             ),
                           ),
                           SizedBox(height: 30),
                           Text(
                             '$containerState Password',
                             style: TextStyle(
                               color: getPasswordStrengthColor(),
                               shadows: [
                                 Shadow(
                                   color: getPasswordStrengthColor().withOpacity(0.5), // Shadow color
                                   offset: Offset(2, 2), // Shadow offset
                                   blurRadius: 2, // Shadow blur radius

                                 ),
                               ],
                             ),
                           )

                         ],
                       ),
                     ],
                   ),
                 ),
                 Container(
                   width: 400,
                   height: 5,
                   color: Colors.grey[900],
                   child: FractionallySizedBox(
                     widthFactor: (calculateStrength(password) / 6) , // Start from 20%
                     alignment: Alignment.centerLeft,
                     child: Container(
                      
                       decoration: BoxDecoration(
                         color: getPasswordStrengthColor(),

                         boxShadow: [
                           BoxShadow(
                             color: getPasswordStrengthColor().withOpacity(0.5),
                             blurRadius: 20.0,
                             offset: Offset(0, 0),
                             spreadRadius: 10
                           ),
                         ],
                       ),
                     ),
                   ),
                 ),
                 SizedBox(
                   width: 400,
                   child: Transform(
                     alignment: Alignment.center,
                     transform: Matrix4.rotationX(3.14159265359), // Mirror effect
                     child: Container(
                       decoration: BoxDecoration(
                         // borderRadius: BorderRadius.only(
                         //   bottomLeft: Radius.circular(20),
                         //   bottomRight: Radius.circular(20),
                         // ),
                         gradient: LinearGradient(
                           begin: Alignment.topCenter,
                           end: Alignment.bottomCenter,
                           colors: [

                             Colors.transparent,
                             Colors.grey[800]!.withOpacity(0.4),
                           ],
                         ),
                       ),
                       height: 100,
                     ),
                   ),
                 ),
               ],
             ),
           ),

         ],
        ),
      ),
    );
  }

  Color getPasswordStrengthColor() {
    switch (containerState) {
      case 'Weak':
        return Colors.red;
      case 'Moderate':
        return Colors.yellow;
      case 'Strong':
        return Colors.green;
      default:
        return Colors.black;
    }
  }
}


```

check strong password with animation 
