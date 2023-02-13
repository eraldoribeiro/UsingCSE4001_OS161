# Running the `cse4001` docker container (Mac OS)

##  Using the Docker Desktop App

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



## Using the terminal(s)

I prefer to use the terminal to work with the `cse4001` Docker container. On my Mac OS, I use a combination of Docker Desktop interactions with command-line instructions. 

1. Start Docker Desktop 

![image-20230213130622046](image-20230213130622046.png)

​	**Figure 5**: Docker dashboard showing the `cse4001` docker container. 

2. Open a Terminal window and start the `cse4001` container.

```bash
docker start -i cse4001
```

![image-20230213175810954](image-20230213175810954.png)

​	**Figure 6**: Starting the `cse4001` Docker container from the terminal. 



3. Boot `OS/161` and work on its codebase to complete assignments. 

![image-20230213180000519](image-20230213180000519.png)

​	**Figure 7**: Booting `OS161`.



4. When working with `OS/161`, it is often useful to open multiple terminals on the same Docker container. To open another terminal on the same active container, type the following command on another terminal. 

 ```shell
 docker exec -it cse4001 bash
 ```

​    ![image-20230213180559154](image-20230213180559154.png)

**Figure 8**: Opening a second terminal running the same docker container. With two terminals open, we can boot `OS161` (from the `os161/root` directory) and we can navigate the source code of assignments that are in the shared directory `/root/workspace`. Note that this `/root/` directory is not `OS161's root` directory. Instead, it is a directory called root inside the `cse4001` Docker container. 

