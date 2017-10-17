# Material-UI

## What is it?

A Set of React Components that Implement Google's Material Design.

##### What is Google's Material Design?

A visual language that synthesizes the classic principles of good design with the innovation and possibility of technology and science.


## Why is it useful?

You can easily add elements from Google's Material Design into your application to make the UI much more sleek and professional looking.


# Installation: 

In your terminal run the following command to install material-ui.

`npm install material-ui`

Material-UI was designed with the Roboto font in mind. So be sure to include it in your project in your css file if you would like the rest of your fonts match theirs.

App.css: 
```
@import url('https://fonts.googleapis.com/css?family=Roboto:300,400,500');

body {
    font-family: Roboto;
}
```


# Getting started: 

The quickest way to get up and running is by using the MuiThemeProvider to inject the theme into your application. 

In your index.js import MuiThemeProvider and wrap the app component with MuiThemeProvider.

```
import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider';

ReactDOM.render(
    <MuiThemeProvider>
        <App />,
    <MuiThemeProvider>
  document.getElementById('app')
);
```

## How easy is it?: 

After you set up MuiThemeProvider to use a raised button in material-ui you simply import RaisedButton from material-ui/RaisedButton and then insert the component into your application. Now you have a fully styled raised button. Its that simple.


```
import React, { Component } from 'react';
import './App.css';
import RaisedButton from 'material-ui/RaisedButton';

class App extends Component {
  render() {
    return (
      <div >
        <RaisedButton label="Click Me" />
      </div>
    );
  }
}

export default App;
```

## Adding a side menu: 

Open up the Menu.js file.

We will need to import Drawer from material-ui/Drawer and List and ListItem from material-ui/List.

```
import Drawer from 'material-ui/Drawer';
import {List, ListItem} from 'material-ui/List';
```

Create a property on state called open and have it set to false. 

```
    this.state = {
        open: false
    };
```

We will need to create a handleToggle method to open and close the side menu. This method should change the open property on state to equal true or false depending on whether it is already open or not. When it is open this.state.open should be true and when it is closed this.state.open should be false. 

```
handleToggle = () => {
    this.setState({
        open: !this.state.open
    });
}
```

In your render under the nav elements insert the Drawer component. This should have a prop of docked equal to false. A prop of width equal to 300. A prop of open equal to this.state.open and a prop of onRequestChange equal to a function that takes open as the parameter and sets state with that.

```
 <Drawer
        docked={false} 
        width={300} 
        open={this.state.open} 
        onRequestChange={(open) => this.setState({open})}>
</Drawer>
```

Within your Drawer component add the List component with three ListItem components. The first list item should have a prop of primaryText that is equal to 'Home'. The second should have the same prop but equal to 'About' and the third should be equal to 'Store'.

```
<Drawer
        docked={false} 
        width={300} 
        open={this.state.open} 
        onRequestChange={(open) => this.setState({open})}>
        <List>
          <ListItem primaryText="Home" />
          <ListItem primaryText="About" />
          <ListItem primaryText="Store" />
        </List>
      </Drawer>
```

You now have a basic side menu. However lets add a nested menu within your side menu. 

Add another prop to the third ListItem called nestedItems that is equal to an object with an array. The first item in the array is a ListItem component with a primaryText prop equal to 'Tops'. 

The second item in the array is a ListItem component with a primaryText prop equal to 'Bottoms'. 

The first item in the array is a ListItem component with a primaryText prop equal to 'Accessories'. 

```
      <Drawer
        docked={false} 
        width={300} 
        open={this.state.open} 
        onRequestChange={(open) => this.setState({open})}>
        <List>
          <ListItem primaryText="Home" />
          <ListItem primaryText="About" />
          <ListItem
            primaryText="Store"
            nestedItems={[
              <ListItem
                primaryText="Tops"
              />,
              <ListItem
                primaryText="Bottoms"
              />,
              <ListItem
                primaryText="Accessories"
              />,
            ]}
          />
        </List>
      </Drawer>
  ```

  You now have a nested menu within your side menu. If we want add a nested menu within the nested menu we would add the nestedItems prop to our 'Accessories' ListItem that is equal to an object with an array and it would have three ListItem components. The first would have a primaryText equal to 'Hats'. The second will be equal to 'Jewelry' and the third 'Scarves'.

  ```
        <Drawer
        docked={false} 
        width={300} 
        open={this.state.open} 
        onRequestChange={(open) => this.setState({open})}>
        <List>
          <ListItem primaryText="Home" />
          <ListItem primaryText="About" />
          <ListItem
            primaryText="Store"
            nestedItems={[
              <ListItem
                primaryText="Tops"
              />,
              <ListItem
                primaryText="Bottoms"
              />,
              <ListItem
                primaryText="Accessories"
                nestedItems={[
                  <ListItem primaryText="Hats" />,
                  <ListItem primaryText="Jewelry" />,
                  <ListItem kprimaryText="Scarves" />,
                ]}
              />,
            ]}
          />
        </List>
      </Drawer>
```


You should now have a working dialog Menu component that you can import and inject into your app.js

```
import React, { Component } from 'react';
import './App.css';
import Menu from './components/Menu';
import DialogBox from './components/DialogBox';

class App extends Component {
  render() {
    return (
      <div >
        <Menu/>

        <DialogBox/>

      </div>
    );
  }
}

export default App;
```

## Adding a dialog modal:

Open up the DialogBox.js file. 

We will need to import Dialog from material-ui/Dialog, FlatButton from material-ui/FlatButton, RaisedButton and material-ui/RaisedButton.

```
import Dialog from 'material-ui/Dialog';
import FlatButton from 'material-ui/FlatButton';
import RaisedButton from 'material-ui/RaisedButton';
```

Create a property on state called open and set it to false. 
```
    state = {
      open: false,
    };
```

Now we need to create a method that will open the modal and a method to close the modal. 

```
      handleOpen = () => {
        this.setState({
          open: true
        });
      };
    
      handleClose = () => {
        this.setState({
          open: false
        });
      };
```

In your return create a raised button with a label of delete that on click will fire the handleOpen method. 

```
        return (
          <div>
            <RaisedButton label="Delete" onClick={this.handleOpen} />
          </div>
        );
```

Below your return create a dialog component with title equal to 'Are you sure you want to delete this?', modal equal to false, open equal to this.state.open, and onRequestClose equal to this.handle close. You can look up what each of these do at http://www.material-ui.com/#/components/dialog. 

Add actions equal to actions and in the next step we will create the actions. 

```
        return (
          <div>
            <RaisedButton label="Delete" onClick={this.handleOpen} />
            <Dialog
              title="Are you sure you want to delete this?"
              actions={actions}
              modal={false}
              open={this.state.open}
              onRequestClose={this.handleClose}
            >             
            </Dialog>
          </div>
        );
```

Above your return in your render, add an array called actions that has two items. The they are both flat buttons with primary equal to true and onClick equal to this.handleClose. The first should have a lable of 'Cancel' and the second should have a label of 'Delete and a keyboardFocused set to true. You can look up what each of these do at http://www.material-ui.com/#/components/flat-button.

```
        const actions = [
          <FlatButton
            label="Cancel"
            primary={true}
            onClick={this.handleClose}
          />,
          <FlatButton
            label="Delete"
            primary={true}
            keyboardFocused={true}
            onClick={this.handleClose}
          />,
        ];

```

You should now have a working dialog modal component that you can import and inject into your app.js

```
import React, { Component } from 'react';
import './App.css';
import DialogBox from './components/DialogBox';

class App extends Component {
  render() {
    return (
      <div >
        <DialogBox/>
      </div>
    );
  }
}

export default App;
``` 


# Resources: 
- https://www.npmjs.com/package/material-ui
- https://github.com/callemall/material-ui/blob/master/src/index.js
- https://material.io/guidelines/#introduction-principles
- https://material.io/icons/
