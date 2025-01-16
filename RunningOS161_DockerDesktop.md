# Running the `cse4001` docker container

## 1. Install Docker on your computer

Skip this step if Docker is already installed on your computer. To install Docker, follow the instructions from the following link: https://www.docker.com/products/docker-desktop/. 

## 2. Get the CSE 4001 Docker container

Now that Docker is installed on your computer, it is time to get the actual container for `CSE4001`. The CSE4001 Docker container is ready to use with Ubuntu Linux installed and packages. You are free to install any other packages that are needed (e.g., GitHub CLI, C/C++ compilers, Python, Conda).   

### The shared folder 
When we install the CS4001 Docker container, the directory `/root/workspace` inside the docker container is mapped to `~/Desktop/CSE4001` in your computer. This is a shared directory between the container file system and your computer's file system. 

This shared folder allows you to keep your source code and development files (i.e., the code of your programming assignments for this class) on your computer while still accessible by the Docker container. The shared folder is called `/root/workspace/` in the Docker file system and is called `cse4001/` in the host computer (i.e., your computer). You can choose to place the shared folder anywhere in your file system. These installation notes assume that the shared directory `CSE4001/` is located in the `~/Desktop` directory. 

### The Docker run command

`Docker run` is the command that we will use to install the CSE4001 container. Before running the command, make sure you are inside the `/Desktop/cse4001` directory or wherever you placed your `cse4001/` that you want to use as the shared directory on your host computer. 

The command's syntax is a bit different for each OS platform, i.e.: 

#### Windows:

```shell
docker run -v "$(PWD):/root/workspace" -ti --name cse4001 eribeirofit/cse4001:latest
```

#### Linux/Intel Mac:

```shell
docker run -v $(PWD):/root/workspace -ti --name cse4001 eribeirofit/cse4001:latest
```

#### M1/M2 Mac:

```shell
docker run -v $(PWD):/root/workspace -ti --platform linux/amd64 --name cse4001 eribeirofit/cse4001:latest
```

Before running one of the above commands, study the example given in the following section. The example that follow are for Mac OS X so some parts might not apply directly to Windows (e.g., running `bash` on the host terminal).

### Example (Intel Mac OS X)

This example shows how to download (and run) docker, and create a shared folder on an **Intel Mac computer**. The shared folder is located at `root/workspace` in the docker container, is located at `~/Desktop/cse4001` in the host computer.  

**Make sure your shell is** **bash**. Before running the `docker run` command, you need to ensure that you are using the bash shell (i.e., the `bash` command-line interpreter). The docker runs on a bash shell. If your terminal runs another shell, type `bash` to start a bash shell on the same terminal. 

Open a terminal. To run the `bash` interpreter, simply type `bash` on your terminal, i.e.: 

![image-20220925140404690](./image-20220925140404690.png)

Go into the shared directory that you created. In this example, the shared directory on the host computer is `~/Desktop/cse4001`. 

```shell
cd ~/Desktop/cse4001/
```

**From inside this directory**, execute the `docker run` command as follows:

```shell
docker run -v $(PWD):/root/workspace -ti --name cse4001 eribeirofit/cse4001:latest
```

The container is a large file so downloading it might take a few minutes. Once it is ready, the terminal will show the following information: 

![image-20220925142155755](./image-20220925142155755.png)

**How can we tell that we are inside a docker container?** 
Well, there are a number of ways to know that, most of them do not involve taking a red or blue pill. In the previous figure, we see that the prompt changed from the original host OS prompt (i.e., `bash-3.2$`) to the container's Linux prompt (i.e., `root@287fd3f34d35#`). This is the clue, at least for this container, that you are inside the Docker container. 

The CSE4001 is now installed and running. This is now your Linux with OS/161 installed. There is (almost) nothing else that needs to be installed for CSE4001. However, if you need to install any other linux packages, you can do it using `apt-get` or similar package managers. 



## Using the terminal(s)

I prefer to use the terminal to work with the `cse4001` Docker container. In general, I use a combination of Docker Desktop interactions (GUI) with command-line instructions (Terminal). 

In the following example, I start the CSE4001 container on one terminal and then I open another terminal on the same container. 

1. Open a Terminal window and start the `cse4001` container.

```bash
docker start -i cse4001
```

![image-20230213175810954](image-20230213175810954.png)

​	**Figure**: Starting the `cse4001` Docker container from the terminal. 



2. Boot `OS/161` and work on its codebase to complete assignments. 

![image-20230213180000519](image-20230213180000519.png)
**Figure**: Boot `OS/161`.


3. When working with `OS/161`, it can be useful to open multiple terminals on the same Docker container. To open another terminal on the same active container, open another terminal windows and type the following command: 

 ```shell
 docker exec -it cse4001 bash
 ```

​    ![image-20230213180559154](image-20230213180559154.png)

**Figure**: Opening a second terminal running the same docker container. In one terminal, we can boot `OS161` (from the `os161/root` directory). In the other terminal, we can navigate the source code of assignments that are in the shared directory `/root/workspace`. Note that this `/root/` directory is not `OS161's root` directory. Instead, it is the root directory inside the `cse4001` Docker container. 









## Using Docker Desktop (GUI)


In addition to the information displayed on the console, you should also see the container listed on the Docker Desktop application, i.e.: 

![image-20220925145526045](./image-20220925145526045.png)

## Using the already installed CSE 4001 Docker container

If the container is already running, just click on the `terminal` icon besides the container name listed on the Docker Desktop. If it is not running, click on the `play` button and then click on the `terminal` icon to open the container's terminal. 



1. Start Docker Desktop.

![image-20230213130622046](image-20230213130622046.png)

​	**Figure 1**: Docker dashboard showing the cse4001 docker container. 



2. Boot the container by clicking on the Docker Desktop's `play` button (GUI's right-hand side).

![image-20230213132308151](image-20230213132308151.png)

​	**Figure 2**: Docker dashboard showing the cse4001 docker container after `play` button is clicked. 



3. Click on the three "vertical dots" on the right-hand side of the GUI to open a terminal: 

![image-20230213132550701](image-20230213132550701.png)

​	**Figure 3**: Opening a terminal window.

4. Change the shell to Bash and work on your OS/161.

![image-20230213132843690](image-20230213132843690.png)

​	**Figure 4**: Calling the OS/161 commands and navigate the directories. 


