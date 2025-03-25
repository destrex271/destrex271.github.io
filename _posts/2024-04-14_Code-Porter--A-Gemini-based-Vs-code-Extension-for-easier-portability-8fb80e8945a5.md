Code-Porter: A Gemini based Vs-code Extension for easier portability

Code-Porter: A Gemini based Vs-code Extension for easier portability
====================================================================

Hello Everyone!

---

### Code-Porter: A Gemini based Vs-code Extension for easier portability

![](https://cdn-images-1.medium.com/max/800/0*_OCQCxov-OeTygj8.jpg)

Hello Everyone!

I am back with another tool that I was able to build using Gemini: The Generative AI Model by Google!

So as we all know Google released its Gemini Model Recently. The model has amazing features and the API is also pretty easy to use. So I though how about I try to make something fun using it! This blog is going to cover that same project that I developed using the Gemini Model.

### The Problem Statement

So till now I am pretty sure that each and every one of us has used LLMs like ChatGPT in one way or another to ease our development workflows, be it in order to understand new code-bases or to improve certain aspects of our code that would have taken a long time to figure out on our own.

Apart from these another application of LLMs has been in porting code snippets from one language to another. This was one of my personal motivations to develop a tool that would help me in porting code snippets between different programming languages. Earlier this would have been a rather tedious task. You would have to develop mappings between various languages to allow this functionality to work and would take a lot of time as well. But LLMs solve this problem very easily by just a simple prompt!

So I decided to convert this into a small yet powerful extension that can be used with various text editors and for starters I decided to go with VSCode.

### Developing the Extension

VS Code has an amazing documentation to develop extensions which you can find [here](https://code.visualstudio.com/api). To get started you need to know very basic Javascript and that’s it!

Let’s walk through the usage of the extension and how everything is running behind the scenes.

To activate the extension you can use Ctrl+Shift+P and then type ‘Convert Code’. This particular command can be used to activate the extension.

#### Stage I: Getting the API key

When you start the extension for the first time it will ask you for your Gemini API key. The VS-Code API provides simple to use fucntions to display elements like input boxes to enable interaction with the user. In this case we utilized the utility as follows:

![](https://cdn-images-1.medium.com/max/800/1*dxePQP8TZN18aKFRFanitQ.png)

As you can see a small text box appears at the top and once the API key is supplied we end up saving it in the local configuration of VS-Code as follows:

#### Stage II: Getting the original code to convert

To make the extension more generic I decided to allow the users to select which part of the code they wanted to port. This seemed to be a better option than converting the entire file.

Before invoking the ‘Convert Code’ function above the user needs to select the parts of code that need to ported. The VSCode API allows us to pick the selected text in any of the active text editors and subsequently save it for further use as shown below:

![](https://cdn-images-1.medium.com/max/800/1*JW1cL0ez86l7Ds1MpTUvbQ.png)

Selected Code & Input box for target Language

This is accomplished by the following snippet:

As you can see we also prompted Gemini to detect the language since we were not able to do that using the VSCode API(which is kinda wired, but do correct me if I am wrong!).

#### Stage III: The Conversion

Now since we have the code snippet and the source language as well we are ready to convert the snippet to the target language. In the previous example I chose the target language as Rust. We are accomplishing this as follows:

![](https://cdn-images-1.medium.com/max/800/1*w53jS5PCJqSH6U_Zmb3r0g.png)

Converted Code displayed in a side panel

As you can see once the code is converted we open up a side panel in VSCode to display the output. Although the output is not pretty enough, it does the job. I am trying to figure out a way to open this as a temporary file without having to save it in the same folder.

There are some nuances associated too like sometimes Gemini might consider the code you are requesting to be converted to be a unsafe and might endup throwing some error which I’ll be fixing in the upcoming releases!

### Conclusion

If you really liked the extension and want to use it in VSCode you can check it out [here](https://marketplace.visualstudio.com/items?itemName=AkshatJaimini.porter) and if you would like to go through the entire codebase you can check it out on [GitHub](https://github.com/destrex271/gemini-porter-extension).

This was a really small application of Generative AI and there a large number of problems that can be solved using this amazing technology! These tools have the ability to define the course of human civilization and its better if we accompany ourselves with them and use them as a brand new set of tools in our arsenal.

Thanks for reading!!

By [Akshat Jaimini](https://medium.com/@destrex271) on [April 14, 2024](https://medium.com/p/8fb80e8945a5).

[Canonical link](https://medium.com/@destrex271/code-porter-a-gemini-based-vs-code-extension-for-easier-portability-8fb80e8945a5)

Exported from [Medium](https://medium.com) on March 25, 2025.