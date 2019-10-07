# A basic template for dockerized Data Science

## Structure
``` text
.
├── README.md
├── docker-compose.yml
└── proj
    ├── Dockerfile
    ├── code
    │   └── hello_world.py
    ├── notebooks
    │   └── test.ipynb
    └── requirement.txt
```
- `Dockerfile` resides inside project directory (Dockerfile:conainter 1 to 1 mapping)
- `proj` as the project directory is mounted into the `dev` container, specified in `docker-compose.yml`

## Usage
``` bash
# build and run
docker-compose up --build

# or build and run in detached mode
docker-compose up --build -d

# destroy container(s)
docker-compose down 
```
- note: before destroying containers, `pip3 freeze > requirement.txt` to save the installed packages

> If container is run in detached mode, to see jupyter token:
``` bash
docker-compose exec dev /bin/bash

# in container:
root@6718e6236e1a:/app jupyter notebook list
```

## Interactive code development
Use your favorite IDE to edit code on local machine but evaluate and test (call `python`, `pytest` etc.) inside container.
