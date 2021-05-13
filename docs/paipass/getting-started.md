# PAI Pass

## Getting Started


The source code for PAI Pass can be found here:

[https://github.com/j1149/catena](https://github.com/j1149/catena)


From there you can build the project by running the following command:

```
 $  docker-compose build
```

(Recommended) If you have linked an AWS account, you can then bring up the project by running,

```
 $ docker-compose up 
```

(Some features may be limited) If you don't have an AWS account linked,  you can bring up the project by running,

```
 $ docker-compose -f docker-compose.yml -f docker-compose.dev.yml up 
```

And to browse the sample site you can visit the following address in your browser:

```
 http://localhost:8000
```
