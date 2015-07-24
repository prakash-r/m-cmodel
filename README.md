# M*C client model

This is the client side framework used for creator live mode. It is desined under **Model-View(Virtual)-Controller** pattern.

## Segmentation

From the pattern we can divide framework into three major parts.

#### Framework Component

1. Controller
  * Controls the entire system comprise of model and view
2. Model
  * JSON meta object that serves information needed for controller to run
3. View
  * An object that communicate with model and rendered HTML dom
  * View also holds the DOM object which is reference object of rendered HTML


Each of the above objects should create for individual creator components

#### Creator Component

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

*Controller* is *Primary Namespace*
***
*ApplicationController* is *Secondary Namespace*
***
*create* is *Constructor function*
***
*model* is *Argument*
***

Similarly to create a form model following will be the convention

```js
Model.FormModel.create({
  type : 1,
  meta : modelJSON
});
```

# Usage

Since all the componenent are tightly coupled we need to create in a ordered sequence

1. Create Model from source meta JSON
2. Create DOM using the above Model
3. Create View with the DOM object
4. Create Controller using Model and View create in previous steps

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

## Factories

Each components are stored in corresponding factory. In Controller Factory you can create all component controllers, similarly for Model and View Factory.

> FactoryClass is the super class of all framework components.

In case of Model Object, ModelFactory is the super class. Form, Report and Field Models are extended from the ModelFactory and this is same for all framework components

## Folder and files

All the files are located under client folder named after framework components. Check out the folder in breif

### controllers

This folder contains all creator component Controllers js and ControllerFactory js

controllerfactory.js
***
It contains staic API to create controller which is a global object under window context
It also contains ControllerFactory object with Model as constructor parameter



## Create a new creator component

To create new component say Form, Report, Field.. follow the bulletins

1. Add component decleration in corresponding js
2. Create API to create instance in each Factory
3. Proceed with the definition


 
