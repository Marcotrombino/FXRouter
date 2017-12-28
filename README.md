<p align="center"><img src="https://github.com/Marcotrombino/FXRouter/blob/master/fxrouterlogo.png"></p>

# FXRouter
[![release](http://github-release-version.herokuapp.com/github/Marcotrombino/FXRouter/release.svg?style=flat)](https://github.com/allure-framework/allure-core/releases/latest)
[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

A simple JavaFX router to switch between application scenes

[Example](#example)

## Download
Get latest release [here](https://github.com/Marcotrombino/FXRouter/releases/latest)

## Supported versions
- 0.0.x - Support for Java 9
- master (1.0.x) - Support for Java 8
### Advantages
You can switch between your scenes from <b>anywhere</b> through a simple method, without worrying about annoying Stage settings.

## Usage
### 1. Bind
Add FXRouter as project dependency and import it from its package:
```java
  import com.github.fxrouter.FXRouter;
```
Connect FXRouter to your application stage: call `bind()` from your main class `start()` method (if you use IntelliJ IDEA) or similar:
```java
FXRouter.bind(this, primaryStage);
```
  ##### You can optionally set application title and size (width, height):
```java
FXRouter.bind(this, primaryStage, "MyApplication", 800, 600);
```
### 2. Set routes
Define your Application routes with a <b>label identifier</b> and its corresponding <b>.fxml</b> screen file:
```java
FXRouter.when("login", "myloginscreen.fxml");
FXRouter.when("profile", "myprofilescreen.fxml");
// ... others
```
##### You can optionally specify the route title and size (width, height):
```java
FXRouter.when("login", "myloginscreen.fxml", "My login screen", 1000, 500);
```
### 3. Switch
Switch routes from anywhere (controllers, services, etc):
```java
FXRouter.goTo("login");     // switch to myloginscreen.fxml
```


### Passing and retrieving data between routes
Your application could need to pass some data to another route and then retrieve those data:
#### Send data from the current scene
`goTo()` accepts two parameters: a <b>route identifier</b> and a <b>`Object`</b>:
##### (Multiples data could be stored on an appropriate Collection)
```java
FXRouter.goTo("profile", "johndoe22");     // switch to myprofilescreen.fxml passing an username
```
#### Get data from the destination scene
`getData()` returns a <b>`Object`</b> which can be cast to appropriate data type:
```java
String username = (String) FXRouter.getData();     // retrieve johndoe22
```

## Example
#### Without FXRouter
A common JavaFX project starter:
```java
package sample;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;

public class Main extends Application {

    @Override
    public void start(Stage primaryStage) throws Exception{
        Parent root = FXMLLoader.load(getClass().getResource("sample.fxml"));
        primaryStage.setTitle("Hello World");
        primaryStage.setScene(new Scene(root, 300, 275));
        primaryStage.show();
    }


    public static void main(String[] args) {
        launch(args);
    }
}
```

#### Using FXRouter 
```java
package sample;

import javafx.application.Application;
import javafx.stage.Stage;
import sample.FXRouter;                                 // import FXRouter

public class Main extends Application {

    @Override
    public void start(Stage primaryStage) throws Exception{
    
        FXRouter.bind(this, primaryStage, "Hello World", 300, 275);    // bind FXRouter
        FXRouter.when("firstPage", "sample.fxml");                     // set "firstPage" route
        FXRouter.goTo("firstPage");                                    // switch to "sample.fxml"
    }


    public static void main(String[] args) {
        launch(args);
    }
}
```

### Switch animation
You can also set an animation type when you switch between routes:
```java
FXRouter.setAnimationType("fade");
```
##### You can optionally specify the animation duration (ms):
```java
FXRouter.setAnimationType("fade", 1200);
```
#### animationType
| AnimationType  | Default duration |
| ------------- | ------------- |
| `fade` | 800  |
