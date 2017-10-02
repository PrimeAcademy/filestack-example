# filestack-example
Example code for file stack upload. The [documentation](https://www.filestack.com/docs/getting-started) is also a great place to look if you have questions.

## Example from previous student

### In Service

You must register with FileStack and use your own API key here

```JavaScript
var fileStack = filestack.init('api key goes here');
```

### In Controller

This specific example also does resizing to `200` by `200`. You may remove that part of the URL in order to simplify your request

```JavaScript
self.pickAvatar = (event) => {    
    var confirm = $mdDialog.confirm()
    .title('Confirm Set Avatar')
    .textContent('this is the text that shows up in the filestack dialog.')
    .ariaLabel('Confirm Set Avatar')
    .targetEvent(event)
    .ok('Proceed')
    .cancel('Cancel');

  $mdDialog.show(confirm).then( () => {
    UserService.fileStack.pick().then((result) => {
      console.log('result', result);
      let convertedUrl = 'https://cdn.filestackcontent.com/' + 
                          'resize=w:200,h:200,f:crop/' +
                          result.filesUploaded[0].handle;
      self.currentClient.client[0].avatar_url = convertedUrl;
      ClientService.editCurrentClient(self.currentClient.client[0]);
    })
    },()=>{});
```

### In View

`vm` is the name of the controller

```HTML
<div id="manage-client-avatar-container" ng-click="vm.pickAvatar($event)">
```
