# E-Portfolio Flutter

## Getting Started

Follow the link and install Flutter and Dart: [Flutter Installation](https://flutter.dev/docs/get-started/install) \
Have at least on way to debug a flutter project. You can use Android Emulator, iOS Simulator, Web, Windows (needs Visual Studio Build Tools) etc. \
You can create and run your first application by following these [steps](https://flutter.dev/docs/get-started/test-drive?tab=vscode). \
\
[Flutter Documentation](https://flutter.dev/docs)

## Usage
Just clone this repository and run 
```Dart
flutter clean
flutter pub get
flutter run //or press debug in your IDE
```
in your source folder.

## Code Snippets needed during the presentation
You can find the demo on [Github Pages](https://jdk-21.github.io/eportfolio-flutter).
### Calculator logic
```Dart
//Calculator logic
  dynamic text = '0';
  double numOne = 0;
  double numTwo = 0;

  dynamic result = '';
  dynamic finalResult = '';
  dynamic opr = '';
  dynamic preOpr = '';
  void calculation(btnText) {
    if (btnText == 'AC') {
      text = '0';
      numOne = 0;
      numTwo = 0;
      result = '';
      finalResult = '0';
      opr = '';
      preOpr = '';
    } else if (opr == '=' && btnText == '=') {
      if (preOpr == '+') {
        finalResult = add();
      } else if (preOpr == '-') {
        finalResult = sub();
      } else if (preOpr == 'x') {
        finalResult = mul();
      } else if (preOpr == '/') {
        finalResult = div();
      }
    } else if (btnText == '+' ||
        btnText == '-' ||
        btnText == 'x' ||
        btnText == '/' ||
        btnText == '=') {
      if (numOne == 0) {
        numOne = double.parse(result);
      } else { 
        numTwo = double.parse(result);
      }

      if (opr == '+') {
        finalResult = add();
      } else if (opr == '-') {
        finalResult = sub();
      } else if (opr == 'x') {
        finalResult = mul();
      } else if (opr == '/') {
        finalResult = div();
      }
      preOpr = opr;
      opr = btnText;
      result = '';
    } else if (btnText == '%') {
      result = numOne / 100;
      finalResult = doesContainDecimal(result);
    } else if (btnText == '.') {
      if (!result.toString().contains('.')) {
        result = result.toString() + '.';
      }
      finalResult = result;
    } else if (btnText == '+/-') {
      result.toString().startsWith('-')
          ? result = result.toString().substring(1)
          : result = '-' + result.toString();
      finalResult = result;
    } else {
      result = result + btnText;
      finalResult = result;
    }

    setState(() {
      text = finalResult;
    });
  }

  String add() {
    result = (numOne + numTwo).toString();
    numOne = double.parse(result);
    return doesContainDecimal(result);
  }

  String sub() {
    result = (numOne - numTwo).toString();
    numOne = double.parse(result);
    return doesContainDecimal(result);
  }

  String mul() {
    result = (numOne * numTwo).toString();
    numOne = double.parse(result);
    return doesContainDecimal(result);
  }

  String div() {
    result = (numOne / numTwo).toString();
    numOne = double.parse(result);
    return doesContainDecimal(result);
  }

  String doesContainDecimal(dynamic result) {
    if (result.toString().contains('.')) {
      List<String> splitDecimal = result.toString().split('.');
      if (!(int.parse(splitDecimal[1]) > 0))
        return result = splitDecimal[0].toString();
    }
    return result;
  }
  ```
### Main UI components
  ```Dart
  Center(
        child: Container(
          width: 400,
          child: Padding(
            padding: EdgeInsets.symmetric(horizontal: 5),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.end,
              children: <Widget>[
                // Calculator display
                SingleChildScrollView(
                  scrollDirection: Axis.vertical,
                  child: Row(
                    mainAxisAlignment: MainAxisAlignment.end,
                    children: <Widget>[
                      Padding(
                        padding: const EdgeInsets.all(10.0),
                        child: Text(
                          '$text',
                          textAlign: TextAlign.left,
                          style: TextStyle(
                            color: Colors.white,
                            fontSize: 100,
                          ),
                        ),
                      )
                    ],
                  ),
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: <Widget>[
                    calcbutton('AC', Colors.grey, Colors.black),
                    calcbutton('+/-', Colors.grey, Colors.black),
                    calcbutton('%', Colors.grey, Colors.black),
                    calcbutton('/', Colors.amber, Colors.white),
                  ],
                ),
                SizedBox(
                  height: 10,
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: <Widget>[
                    calcbutton('7', Colors.grey, Colors.white),
                    calcbutton('8', Colors.grey, Colors.white),
                    calcbutton('9', Colors.grey, Colors.white),
                    calcbutton('x', Colors.amber, Colors.white),
                  ],
                ),
                SizedBox(
                  height: 10,
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: <Widget>[
                    calcbutton('4', Colors.grey, Colors.white),
                    calcbutton('5', Colors.grey, Colors.white),
                    calcbutton('6', Colors.grey, Colors.white),
                    calcbutton('-', Colors.amber, Colors.white),
                  ],
                ),
                SizedBox(
                  height: 10,
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: <Widget>[
                    calcbutton('1', Colors.grey, Colors.white),
                    calcbutton('2', Colors.grey, Colors.white),
                    calcbutton('3', Colors.grey, Colors.white),
                    calcbutton('+', Colors.amber, Colors.white),
                  ],
                ),
                SizedBox(
                  height: 10,
                ),
                Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: <Widget>[
                    //this is button Zero
                    ElevatedButton(
                      onPressed: () {
                        calculation('0');
                      },
                      style: ElevatedButton.styleFrom(
                        padding: const EdgeInsets.fromLTRB(34, 25, 128, 25),
                        shape: StadiumBorder(),
                        primary: Colors.grey,
                      ),
                      child: Text(
                        '0',
                        style: TextStyle(fontSize: 25, color: Colors.white),
                      ),
                    ),
                    calcbutton('.', Colors.grey, Colors.white),
                    calcbutton('=', Colors.amber, Colors.white),
                  ],
                ),
                SizedBox(
                  height: 10,
                ),
              ],
            ),
          ),
        ),
      ),
```
