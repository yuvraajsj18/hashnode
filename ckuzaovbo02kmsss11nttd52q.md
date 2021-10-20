## How to Save User's Data Persistently in Web Browser Using Local Storage

In this article, we will learn how to use Local Storage to save data persistently in the browser using Local Storage.

### Prerequisite

You will just need familiarity with basic JavaScript and HTML.

The best way to go through the article is to open your code editor and code along with me.

So, let's start!

# What is Local Storage?

*LocalStorage* is a property of *windows* object, it allows us to store key-value pairs in a web browser.

The localStorage's data has no expiration date. 

The data will not be deleted when the browser is closed and will be available whenever you open the same web page.

Each Protocol-Domain combination will have different local storage, which means, `[http://example.com](http://example.com)` and `[https://example.com](https://example.com)` will not share their local storage property.

## Why use Local Storage?

LocalStorage is generally used to save a user's preferences, theme settings, login information, auth tokens. You can store any kind of information you want.

# Using Local Storage

Let's start by creating a simple web page with a button and a heading 💻

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Local Storage</title>
</head>
<body>
    <button id="count-btn">Count</button>
    <h1 id="clicks-count">0</h1>

    <script src="main.js"></script>
</body>
</html>
```

We have given both `button` and `h1` tags an id to access them in the JavaScript ****file.
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1634715001482/GlKC7N_Rv.png)

This is how our web page looks, we want to increase the number by 1 each time the **Count** button is pressed.

Let's create a JavaScript file *main.js* and the following code **to implement this behavior:

```jsx
document.querySelector('#count-btn').addEventListener('click', (e) => {
    const countElement = document.querySelector('#clicks-count');
    const count = Number(countElement.innerText) + 1;
    document.querySelector('#count-btn').addEventListener('click', (e) => {
    const countElement = document.querySelector('#clicks-count');
    const count = Number(countElement.innerText) + 1;
    localStorage.setItem('count', count);
    countElement.innerText = count;
});
    countElement.innerText = count;
});
```

We added an event listener for the **click** action on the button, whenever the button is clicked we access the value of **h1**, increment it by 1, and then update the **h1** again.

Now, the page is behaving the way we want:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1634715050804/wz8eVIRNE.png)

But there's a problem! Try refreshing the page and the count resets to 0.

Now we will use local storage to save this count so that we start from the same number we reached before refreshing or closing the browser.

**Setting count in LocalStorage**

Use the `localStorage.setItem(key, value);` in the event listener we created before:

```jsx
document.querySelector('#count-btn').addEventListener('click', (e) => {
    const countElement = document.querySelector('#clicks-count');
    const count = Number(countElement.innerText) + 1;
    localStorage.setItem('count', count);
    countElement.innerText = count;
});
```

This will set a key `count` in the local storage and update it each time we press the button.

You can check it by opening the inspect element (Control+Shift+I on windows, Command + Shift + I on mac) and going into the application tab, and selecting Local Storage from the left menu:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1634715073540/CNRMESjl-.png)

Try refreshing the page again, it still starts from 0, that's because we have saved the value but we also need to set the previous value of count to the initial value when the page loads:

We will use the `localStorage.getItem(key);` to access a value of a key from localStorage.

Edit the *main.js* to use `getItem` function:

```jsx
document.querySelector('#clicks-count').innerText = localStorage.getItem('count') ?? 0;

document.querySelector('#count-btn').addEventListener('click', (e) => {
    const countElement = document.querySelector('#clicks-count');
    const count = Number(countElement.innerText) + 1;
    localStorage.setItem('count', count);
    countElement.innerText = count;
});
```

The first line checks if a key 'count' exists in the local storage, if true it sets the heading to that number otherwise it set it to 0.

You could also have used an `if` condition for this but here we are using the more succinct `??` operator.

`??` - The [nullish coalescing operator (??)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined and otherwise returns its left-hand side operand.

And with this, we are done with our web page. Try refreshing or closing the browser and the count will still start from the last value.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1634715091682/8gfEysWyn.png)

# Local Storage Methods Summary

- **`localStorage.setItem(key, value);`**
    
    Adds a key and value pair to local storage.
    
- `**const cat = localStorage.getItem(key);**`
    
    Gets a value for a key from the local storage.
    
- `**localStorage.removeItem(key);**`
    
    Deletes a key-value pair from the local storage.
    
- **`localStorage.clear();`**
    
    Deletes all key-value pairs from the local storage.
    

# Conclusion

Now that you know how to use localStorage, try using it in your next project.

Here are a few project ideas for beginners to try out localStorage:

- Todo App
- Notes App
- Shopping List App

I hope you found this article helpful! Thanks for reading.