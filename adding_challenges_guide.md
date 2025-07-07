## How to add challenges and deploy onto CTFd
### 1. Create the challenge folder for a new challenge or modify existing challenge
File structure:
```
challenge_name
├── README.md
├── challenge.yml
├── docker-compose.yml
├── dist
│   └── challenge_name.zip  # files to be given to players
├── solve
│   └── README.md          
│   └── other files e.g. solve.py          
└── src
    ├── Dockerfile          
    └── files needed for hosting (e.g. flag.txt, chall)
```
Important notes on `challenge.yml`:

- `type: standard` not `type: fixed` for fixed score challenges
- `attribution` is not supported. use this instead
```
tags:
    - author name 
``` 
- for 
```files:
    - dist/filename
``` 
filename must exist or ctfcli will crash 


#### For challenges that need to be hosted:
- `Dockerfile` and `docker-compose.yml` must be present
- Test if `docker compose up` can spin up the challenges before submitting
- Add the content `your_challenge_category/your_challenge_name/docker-compose.yml` to `docker-compose.yml` 
Example add on:
```
services:
  yadayadayada:
    blah blah blah 
# add this part
  general-napping_cat:
    container_name: general-napping_cat
    build:  general-skills/napping-cat/src # remember to change this
    ports:
      - 12344:5000 # use port 5000 if you are using pwn.red 
    privileged: true  # uncomment this if you are using pwn.red 
``` 
### 2. Update `.ctf/config` file
If you created a new challenge (eg. `general-skills/napping-cat/`) Add this line to the end of `.ctf/config`
```
general-skills/napping-cat/ = general-skills/napping-cat/
```
#### DO NOT MODIFY ANYTHING ELSE INSIDE `.ctf/config`

### 3. Push to main 
Github actions workflow will deploy the challenges to [CTFd training platform](https://training.sieberr.live) (hopefully)

Success!