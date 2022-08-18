# ngModel

## Learning Goals

- Explain the ngModel directive.

## Introduction

As discussed previously, `ngModel` gives us the ability to have 2-way data
binding, which means that our view reacts to the values of the associated
variable in our model, and the associated variable in our model takes on the
value of the associated element in our view.

## Example 

Let's consider for example that we want to add a "message preview" to our
application, where we show the user the message they are typing in a view
similar to how it will be displayed once they actually send it. We would like to
do this without asking the user to click a "preview" button. In other words, the
preview should update in real-time as the user types their message.

Since `ngModel` is a directive from Angular's "Forms" package, we first need to
import that module in our `app.module.ts` file. Add the following TypeScript
import:

```typescript
import { FormsModule } from "@angular/forms";
```

And then add the following Angular import:

```typescript
  imports: [
    BrowserModule,
    FormsModule
  ],
```

Now we can add a variable in our controller, which in our case is
`send-message-component.component.ts`, and we add a `messageString` variable:

```typescript
import { Component, OnInit } from "@angular/core";

@Component({
  selector: "app-send-message-component",
  templateUrl: "./send-message-component.component.html",
  styleUrls: ["./send-message-component.component.css"],
})
export class SendMessageComponentComponent implements OnInit {
  messageString: string;

  constructor() {}

  ngOnInit(): void {}
}
```

Now we modify our view to tell is that the input text box should be associated
with the `messageString` variable:

```html
<input
  type="input"
  class="form-control"
  placeholder="Type a message"
  [(ngModel)]="messageString"
/>
```

This means that we now know that any time the value of the input box changes,
Angular will make sure that the value of the `messageString` variable in our
model also changes. Since we can use the `{{}}` notation to display the value of
any of our model variables, we can now add the following row to our display to
show a preview of the user's message as they type it:

```html
<div class="row">
  <div class="col-3 p-3">Message Preview</div>
  <div class="col-9 p-3">
    <div class="col-10 p-3 border rounded-5">
      <span>{{messageString}}</span>
    </div>
  </div>
</div>
```

Our `send-message-component.component.html` view now looks like this:

```html
<div class="container">
  <div class="row">
    <div class="col-10 p-3">
      <input
        type="input"
        class="form-control"
        placeholder="Type a message"
        [(ngModel)]="messageString"
      />
    </div>
    <div class="col-2 p-3">
      <div class="float-end">
        <button class="btn btn-primary">Send</button>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col-3 p-3">Message Preview</div>
    <div class="col-9 p-3">
      <div class="col-10 p-3 border rounded-5">
        <span>{{messageString}}</span>
      </div>
    </div>
  </div>
</div>
```
