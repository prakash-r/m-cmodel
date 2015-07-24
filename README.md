# M*C client model

This is the client side framework used for creator live mode. It is desined under **Model-View(Virtual)-Controller** pattern.

## Segmentation

From the pattern we can divide framework into three major parts.

1. Controller
  * Controls the entire system comprise of model and view
2. Model
  * JSON meta object that serves information needed for controller to run
3. View
  * An object that communicate with model and rendered HTML dom
  * View also holds the DOM object which is reference object of rendered HTML


Each of the above objects should create for individual creator components

- Application
- Form
- Report
- Page

## Naming convention

The syntax is divided into four segments

1. Primary Namespace
  - Framework component is the primary namespace Ex: Controller, Model.. etc
2. Secondary Namespace
  - Creator components will be the secondary components Ex. FormModel, ApplicationView... etc
3. Constructor function
  - Function to create the instance Ex: create, get... etc
4. Arguments
  - Parameters to the constructor funciton Ex: model, type.. etc


Lets take the example for Application Controller,

```js
Controller.ApplicationController.create({
  model : {appname:"IT ASSET",linkname:"it-asset"};
});
```
Here
*Controller* is *Primary Namespace*
*ApplicationController* is *Secondary Namespace*
*create* is *Constructor function*
*model* is *Argument*

Similarly to create a form model following will be the convention

```js
Model.FormModel.create({
  type : 1,
  meta : modelJSON
});
```

# Usage

Since all the componenent are tightly coupled we need to create in a ordered sequence

1. Create Model
2. Create Controller using Model create in previous step
1. Create DOM using the above Model
4. Create View with the DOM object

Here is the example usage code to create form controller

```js
var formModel = Model.FormModel.create({
  meta : sourceJSON
});

var formDOM = DOM.FormDOM.get({
  model : formModel
});

var formView = View.FormView.create({
  dom : formDOM
});

var formController = Controller.FormController.create({
  model : formModel,
  view : formView
});
```
