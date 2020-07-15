# NumberPickerRedux [![Build Status](https://travis-ci.com/MeixDev/NumberPickerRedux.svg?branch=master)](https://travis-ci.com/MeixDev/NumberPickerRedux) [![Coverage Status](https://coveralls.io/repos/github/MeixDev/NumberPickerRedux/badge.svg?branch=master)](https://coveralls.io/github/MeixDev/NumberPickerRedux?branch=master)

Update of MarcinusX's NumberPicker package for my personal purposes.

NumberPickerRedux's NumberPicker is a custom widget designed for choosing an integer or decimal number by scrolling spinners.

It is possible to use NumberPicker as a standalone widget as well as in NumberPickerDialog.

As the project is not released on [pub.dev](https://pub.dev), you must add it as a dependency of your project the following way:

```yaml
dependencies:
  number_picker_redux:
    git:
      url: git@github.com:MeixDev/NumberPickerRedux.git
```

if you get a `Host key verification failed` when trying to pub get, you should add GitHub as a known host:
`ssh-keyscan github.com >> ~/.ssh/known_hosts`

![vertical](https://raw.githubusercontent.com/MarcinusX/NumberPicker/master/example/screenshots/gif_example.gif)

## Getting Started
#### Creating NumberPicker Widget

```dart
new NumberPicker.integer(
                initialValue: 50,
                minValue: 0,
                maxValue: 100,
                onChanged: _handleChange)
```

#### Creating NumberPickerDialog (use in material's showDialog method)
```dart
new NumberPickerDialog.decimal(
          minValue: 1,
          maxValue: 10,
          initialDoubleValue: _currentPrice),
```

### Usage examples
See examples directory for full examples.

#### Standalone widget
![vertical](https://raw.githubusercontent.com/MarcinusX/NumberPicker/master/example/screenshots/gif_widget.gif)
```dart
class _MyHomePageState extends State<MyHomePage> {
  int _currentValue = 1;

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      body: new Center(
        child: new Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            new NumberPicker.integer(
                initialValue: _currentValue,
                minValue: 0,
                maxValue: 100,
                onChanged: (newValue) =>
                    setState(() => _currentValue = newValue)),
            new Text("Current number: $_currentValue"),
          ],
        ),
      ),
      appBar: new AppBar(
        title: new Text(widget.title),
      ),
    );
  }
}

```

#### Dialog
![vertical](https://raw.githubusercontent.com/MarcinusX/NumberPicker/master/example/screenshots/gif_dialog.gif)
```dart
class _MyHomePageState extends State<MyHomePage> {
  double _currentPrice = 1.0;

  void _showDialog() {
    showDialog<int>(
      context: context,
      builder: (BuildContext context) {
        return new NumberPickerDialog.decimal(
          minValue: 1,
          maxValue: 10,
          title: new Text("Pick a new price"),
          initialDoubleValue: _currentPrice,
        );
      }
    ).then((int value)) {
      if (value != null) {
        setState(() => _currentPrice = value);
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      body: new Center(
        child: new Text("Current price: $_currentPrice \$"),
      ),
      appBar: new AppBar(
        title: new Text(widget.title),
      ),
      floatingActionButton: new FloatingActionButton(
        child: new Icon(Icons.attach_money),
        onPressed: _showDialog,
      ),
    );
  }
}
```