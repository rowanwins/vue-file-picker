
## About
A fairly minimal file picker & drop area which aims to stay out of the way of your application. 

[Demo here](https://rowanwins.github.io/vue-file-picker/)

We handle
- a html [file input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file)
- a js [drag & drop area](https://developer.mozilla.org/en-US/docs/Web/Events/drop)

You handle
- What happens after files are recieved, eg
  - uploading
  - presentation of the UI

## Install
````
npm install vue-file-picker --save
````

## Usage

### Props
| Name          | Type           | Default  | Description  |
| ------------- | -------------- | --------- | ----- |
| id            | string (**required**) | null  | id of the wrapping div |
| accept        | string [details](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#accept) | `*/*` | A string that defines the file types the file input should accept |
| allowMultiple | boolean [details](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#multiple) | false | Allows the user to select more than one file |


### Slots
| Name    | Description  |
| ------- | ------------- |
| icon    | Something to display above the label, eg an `i` or `svg` |
| label   | A string to display as the label |


### Events
| Name    | Description  |
| ------- | ------------- |
| vfp-file-added(FileList)| Triggered by the addition of a file/s, recieves an [FileList](https://developer.mozilla.org/en-US/docs/Web/API/FileList) as the argument. |
