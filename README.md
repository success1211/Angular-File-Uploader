Angular file uploader is an Angular 2/4/5 file uploader module with Real-Time Progress Bar, Angular Universal Compatibility and multiple themes which includes Drag and Drop and much more.

### Install
```
npm i angular-file-uploader
```
### Usage
- Bootstrap.min.css is required.
  Include 
  ```html
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
  ```
  in your index.html.
- Import FileUploadModule inside your app.module.ts 
  ```javascript
  import { FileUploadModule } from "angular-file-uploader";
  ```
  ```javascript
  @NgModule({
    imports: [
        ...,
        FileUploadModule,
        ...
    ]
  })
  ```
##### Example-1 ( with minimal configuration )
  ```html
  <angular-file-uploader
        [config]="afuConfig">
  </angular-file-uploader>
  ```  
  ```javascript
  afuConfig = {
      uploadAPI: {
        url:"https://example-file-upload-api"
      }
  };
  ```
##### Example-2 ( with all available configuration )
  ```html
  <angular-file-uploader 
        [config]="afuConfig"
        [resetUpload]=resetVar
        (ApiResponse)="DocUpload($event)">
  </angular-file-uploader>
  ``` 
  ```javascript
  afuConfig = {
      multiple: false,
      formatsAllowed: ".jpg,.png",
      maxSize: "1",
      uploadAPI:  {
        url:"https://example-file-upload-api",
        headers: {
       "Content-Type" : "text/plain;charset=UTF-8",
       "Authorization" : `Bearer ${token}`
        }
      },
      theme: "dragNDrop",
      hideProgressBar: true,
      hideResetBtn: true,
      hideSelectBtn: true
  };
  ``` 

| **Properties**             | **Description**                                                                                                                                                                       | **Default Value**                          |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
| config : object            | It's a javascript object. Use this to add custom constraints to the module. All available key-value pairs are given in example 2.For detailed decription refer the table below.        | {}                              |
| ApiResponse:EventEmitter   | It will return the response it gets back from the uploadAPI. Assign one custom function ,for example " DocUpload($event) " here, where " $event " will contain the response from the api.                                                           |                                        |
| resetUpload : boolean      | Give it's value as " true " whenever you want to clear the list of  uploads being displayed. It's better to assign one boolean variable ('resetVar' here)to it and then  change that variable's value. Remember to change 'resetVar' value 'true' to 'false' after every reset. | false                                  |


| **[config]**               | **Description**                                                                                                                                                                       | **Default Value**                      |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
| multiple : boolean         | Set it as " true " for uploading multiple files at a time and as " false " for single file at a time.                                                                                 | false                                  |
| formatsAllowed : string    | Specify the formats of file you want to upload.                                                                                                                                       | '.jpg,.png,.pdf,.docx, .txt,.gif,.jpeg'|
| maxSize : number           | Maximum size limit for files in MB.                                                                                                                                                   | 20 MB                                  |
| uploadAPI.url : string     | Complete api url to which you want to upload.                                                                                                                                         | undefined                              |
| uploadAPI.headers : {}     | Provide headers you need here.                                                                                                                                                        | {}                                     |
| theme : string             | Specify the theme name you want to apply. Available Themes: ' dragNDrop ', ' attachPin '                                                                                                                | If no theme or wrong theme is specified, default theme will be used instead.|
| hideProgressBar:boolean    | Set it as " true " to hide the Progress bar. | false |
| hideResetBtn:boolean       | Set it as " true " to hide the 'Reset' Button. | false |
| hideSelectBtn:boolean      | Set it as " true " to hide the 'Select File' Button. | false |

---
##### A Better Way to reset the module
You have seen that by using 'resetUpload' property, you can reset the module easily, however if you need to reset more than one time, there's a better way of doing that( bcoz in 'resetUpload' property, you have to make it as false in order to use it again):-

###### Example-3
  ```html
  <angular-file-uploader #fileUpload1
        [config]="afuConfig"
        [resetUpload]=resetVar
        (ApiResponse)="DocUpload($event)">
  </angular-file-uploader>
  ```
  - Assign one local reference variable (here 'fileUpload1') to the component.
  - Now use this local reference variable in your xyz.component.ts file.
    ```javascript
        @ViewChild('fileUpload1')
        private fileUpload1:  FileUploadComponent;
    ```
    - Remember to import ViewChild and FileUploadComponent properly in your component.
      ```javascript
        import { ViewChild } from '@angular/core';
        import { FileUploadComponent } from "angular-file-uploader";
      ```
  - That's it.....all done, now just use
    ```javascript
        this.fileUpload1.resetFileUpload();
    ```
    to reset the module hassle-free anytime.

##### Points to note:
- Files are uploaded in FormData format.

### Coming Soon:
- More themes.
- More customization options.
