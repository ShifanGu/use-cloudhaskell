The purpose of this project is to provide a baseline demonstration of the use of cloudhaskell in the context of the
code complexity measurement individual programming project. The cloud haskell platform provides an elegant set of
features that support the construction of a wide variety of multi-node distributed systems commuinication
architectures. A simple message passing abstraction forms the basis of all communication.

This project provides a command line switch for starting the application in master or worker mode. It is implemented
using the work-pushing pattern described in http://www.well-typed.com/blog/71/. Comments below describe how it
operates. 

To use, build and do somethign like the following to start some clients:

```
stack exec use-cloudhaskell-exe worker localhost 8000 &
stack exec use-cloudhaskell-exe worker localhost 8001 &
stack exec use-cloudhaskell-exe worker localhost 8002 &
stack exec use-cloudhaskell-exe worker localhost 8003 &
```
Or alternative, a docker-compose.yml file is provided that supports the launching of a set of workers:

```
docker-compose up
```

And then start the manager as follows:

```
stack exec use-cloudhaskell-exe manager localhost 8005 100
```

To understand the ouput, consult the code.

__Docker-Compose__

The basic architecture of the work stealing pattern has a manager node as a central component surrounded by a set of
worker nodes. Each worker node is presumed to execute on a different node such that the total computational capacity of
the worker node set are aailable to us to deliver processing. 

Launching worker nodes individually is inconvenient and so I have added a `docker-compose.yml` file to the project. To
launch a set of worker nodes, run:

```
docker-compose up
```

One may now launch a manager node to passwork for these nodes:

``` bash
stack exec use-cloudhaskell-exe manager localhost 8085 100
```

where the final parameter is the size of the number range (see the code to see the specifics on what the project is
calculating).

This project is a companion to the REST service client [use-haskell-client](https://bitbucket.org/esjmb/use-haskell-client) and [use-haskell-api](https://bitbucket.org/esjmb/use-haskell-api).