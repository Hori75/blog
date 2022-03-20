---
layout: post
title:  "Refactoring a React Project"
author: hori75
date:   2022-03-20 22:00:00 +0700
background: '/images/refactor2.png'
excerpt_separator: <!--more-->
---

Initializing react project and working from there could be messy.
<!--more-->
Not only you have to setup from scratch, you have to build components itself.
If not organized, the code could be turned into a mess due to javascript doesn't care the project structure itself.

In this post, I'd like to share my story on working a project and refactoring process.

### Starting Project

At the start of development, I initialized the project from [Create React App](https://create-react-app.dev/).
Then the CI/CD and the server is setup, but this is out of scope on this post.

Actually, there are few member from the team that just started working on react.
They are learning on the fly and the project was just an initial from Create React App.
So the results are a bit messy from my own view.

![Example of code](/images/refactor1.png)

Apart from that, we still use javascript and haven't used linter.
So I planned to refactor so they could work on it properly.

### Using Typescript

The first step is to use Typescript. The reason behind that is to create more strictier.
Why we need more strictier rule, because javascript is so flexible, it won't check the type expected on function.
Other than that, we would like to prevent more errors that could be avoided by strictier rule.

### Applying Eslint

Second step is to apply eslint. It's easy to initialize the project.
You could set it to check for warning, syntax errors, and enforce a codestyle.
Also, there is a popular codestyle you could pick to follow. 
The one annoying thing is that I have to disable preflight check so the conflicting dependencies doesn't block any action.
So far, there isn't any problem regarding the conflicting packages.

### Seperate the Component Concerns

I reorganize the components so other team members could work on the code more orderly.
This is done by seperating the client (to get backend data), models (to set types of data), and Layouts 
(which contains only MainLayout for now).

![Example of structure](/images/refactor2.png)

Apart from that, I also seperate the routing from the `App.tsx` so the we won't need to make changes on the file.

Heres what is like, more or less

```
import React from 'react';
import { Route, Routes } from 'react-router-dom';
import {
  ...
} from './components';

const Router = () => {
  return (
    <Routes>
      <!-- insert route here -->
    </Routes>
  );
};
export default Router;
```

The next step to be (hopefully) done on the project is to seperate other smaller components from a page so we could reuse it.
After that, the page component shall be moved to it's own directory.

### Advice came too late

While I was complaining about react's weird coverage report file, my friend actually recommended me to use nextjs instead of
the vanila `create-react-app` to initialize the project. I haven't done it because it's the first time setting up a react project.
One of the advantages I see are it's routing system are completely based on `pages` directory, so we don't really need to create our own.

### Lesson Learned

When initializing a project is simple enough. The structure must be set properly and hence the refactor was done so other team 
members who new to react could work on it more easily.
