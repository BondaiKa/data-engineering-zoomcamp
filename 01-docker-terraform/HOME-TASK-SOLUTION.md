# Solution for `Module 1 Homework: Docker & SQL`

## Provided home description:

> In this homework we'll prepare the environment and practice Docker and SQL
> When submitting your homework, you will also need to include a link to your GitHub repository or other public code-hosting site.
> This repository should contain the code for solving the homework.
> When your solution has SQL or shell commands and not code (e.g. python files) file format, include them directly in the README file of your repository.

## Installation
I skippe all explanation and tutorials how to install Docker etc and writting my own steps. My intrsuctions will be for Mac

1. Install Docker into Mac [link](https://docs.docker.com/desktop/setup/install/mac-install/)
2. Login into Docker
3. Run following command:
    ```bash
    docker-compose up --build
    ```

## Useful tricks and commands that I used during home assigment
- To get container id I used
    ```bash
    docker ps
    ```
- To add additional container (I called it python in docker-compose.yaml `python`) for question 1 without restarting `Postgres` and `pgadmin` other container I used next command. 
    ```bash
    docker-compose up -d --no-deps --build python 
    ```
    ❗️ To avoid exiting container immediatelly with code 0 - you need to run some dummy task in order to keep container running (e.g. `command: ["tail", "-f", "/dev/null"]`)

## Answers on written question

### Question 1. Understanding docker first run
> Run docker with the python:3.12.8 image in an interactive mode, use the entrypoint bash.
> What's the version of pip in the image?
> 
> 24.3.1
> 24.2.1
> 23.3.1
> 23.2.1

1. So what I did is I added additional container with running dummy process to not shut down container
    ```yaml
    python:
        container_name: python
        image: python:3.12.8
        command: ["tail", "-f", "/dev/null"]
    ```
2. Then I attached to container to bash:
    ```bash
    docker exec -it python bash  
    ```
3. Get pip version 😁
    ```bash
    root@7694c7336585:/# python3.12 -m pip --version
    pip 24.3.1 from /usr/local/lib/python3.12/site-packages/pip (python 3.12)
    ```
So the answer is `24.3.1`