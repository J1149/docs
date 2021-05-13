# PAI Pass Production Process

So the simplified version is,

- I develop code
- I test it locally
- I commit the changes then push them to github
- I pull the changes to the corresponding EC2 instance (there are three; one for the frontend; one for the backend; one for the admin) where PAI Pass is running in production
- I build the image(s) on that EC2 instance
- I run it on that EC2 instance

## Login


### Backend

You can login with 

```bash
ssh -i paipass-keypair.pem ubuntu@3.228.5.171 
```

If it doesn't place you in the correct directory you can run,

```bash
cd /media/nvme/20200508/paipass3/paipass
```

### Frontend

You can login with 

```bash
ssh -i paipass-keypair.pem ubuntu@52.206.91.212
```

If it doesn't place you in the correct directory you can run,

```bash
cd ~/paipass
```


### Admin
You can login with 

```bash
ssh -i paipass-keypair.pem ubuntu@3.224.135.77
```

If it doesn't place you in the correct directory you can run,

```bash
cd ~/paipass
```


## Build

### Backend 
You can  build the backend with the following
```bash
git pull origin
sudo docker-compose -f docker-compose.backend.yml build
```

### Frontend
```bash
git pull origin
sudo docker-compose -f docker-compose.frontend.yml build
```


### Admin
This should correct (I pulled it from the bash history) but I haven't done it in awhile and I don't want to risk screwing with it at this point.

```bash
git pull origin
sudo docker-compose up --build admin
```



#### Issues

There isn't nearly enough space to make a mistake on the build so you will eventually have to run

```bash
sudo docker system prune
```

when you make that mistake


## Run 
### Backend
To stand it up run,
```bash
sudo docker-compose -f docker-compose.backend.yml up -d
```

### Frontend
To stand it up run,
```bash
sudo docker-compose -f docker-compose.frontend.yml up -d
```
### Admin
This should correct (I pulled it from the bash history) but I haven't done it in a very long time and I don't want to risk screwing with it at this point.

```bash
sudo docker-compose up --build admin
```

