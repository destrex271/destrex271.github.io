Rust Tool/API to generate and serve audio files to clients — Part I

Rust Tool/API to generate and serve audio files to clients — Part I
===================================================================

Well, we all at some point used youtube to mp3 conversion websites like ytmp3, etc, but did you ever want to get even slightly close to…

---

### Building a Tool/Web-API in Rust to generate and serve audio files— Part I

![](https://cdn-images-1.medium.com/max/800/1*6qVv2ZttyLNYL8E-P4HuMw.png)

Well, we all at some point used youtube to mp3 conversion websites like ytmp3, etc, but did you ever want to get even slightly close to making something like that?

That is what I wanted to do, so I started this simple project called [*rytaud*](https://github.com/destrex271/rytaud)*.* In part I made a simple web server that utilizes the youtube-dl CLI tool to get the mp3 file and serve it to the user.

### Setting up the server

To setup the web server I used the [*actix-web*](https://actix.rs/) framework in rust and setup the required endpoints with their function calls. I used actix because at first I wanted to keep my project simple and writing my own server configuration would have deviated me from the actual aim. While developing anything on your own you should try to follow the KISS principle as much as possible, you can always customise things latter.

Here is the code for my server:

As you can see I have setup three endpoints out of which the delete\_vid endpoint is not of concern as of now. The endpoint POST ‘/download\_audio’ triggers the youtube-dl utility interface that we will look into later. It returns a reference to the ‘/audio’ endpoint which is an actix\_files endpoint acting as a file hosting service in a way.

### CLI interfacing

To interface with the youtube-dl CLI I used the std::Command library available in rust as follows:

This function calls the youtube-dl cli and generates the mp3 file according to the key provided by the user. This file is being stored in the root of the program as of now. The HTTP server returns the path as ‘/audio/file.mp3’ which the user can then access to use the audio file.

### Containerization

I also decided to containerize the application and setup a github workflow to automatically build and deploy the image as a package on github for public use. The docker image is a multi stage build with the rust image to compile the project and a debian bullseye image to run the compiled program.

### Goals for the next stages

#### Imrpoved Storage

Storing a large number of audio files on a single system and that too in a container is not a good practice but since I was unable to get any other cloud storage services I decided to go with it and instead implement a background service that deletes all the mp3 files in 24 hours, that can be seen in the code for the server, but remember the project is still in its initial stages. So as of now, I need to find a storage service that abstracts all of this for me or design something like that on my own.

#### Writing the download tool

youtube-dl is an amazing tool but the end goal of this project is to implement that utility in my own way to give me more control and optimize the entire process because the speed at which youtube-dl downloads the file is pretty slow and it affects the overall performance of the API. The tool should also allow users to get audio from other platforms as well.

#### Reduce the Image size

The docker image for the project is pretty huge as of now, around 912 MB. I need to find a way to reduce this size further. Also I want to setup an orchestration service for deploying the project like Kubernetes but before that I need to fix the above mentioned problems to optimize my builds.

### Conclusion

So that was it for Part I. The project needs more improvements. I hope you guys test out the project. Suggestions and feedbacks are always welcome. If you wish to contribute to the project please checkout the [*GitHub repository*](https://github.com/destrex271/rytaud)*.*

A [*docker image*](https://github.com/destrex271/rytaud/pkgs/container/rytaud) for the same is available on github packages, so if you want to look into that you are welcome to do so.

By [Akshat Jaimini](https://medium.com/@destrex271) on [December 30, 2022](https://medium.com/p/f5297e064564).

[Canonical link](https://medium.com/@destrex271/rust-tool-api-to-generate-and-serve-audio-files-to-clients-part-i-f5297e064564)

Exported from [Medium](https://medium.com) on March 25, 2025.