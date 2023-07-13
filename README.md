# DistLedger (Distributed Systems @ IST)
## Final delivery grade 17/20

### Team Members

 
| Number | Name              | User                             | Email                                       |
|--------|-------------------|----------------------------------|---------------------------------------------|
| 99540  | Pedro Lameiras    | <https://github.com/JLameiras>   | <mailto:pedrolameiras@tecnico.ulisboa.pt>   |
| 99228  | Gonçalo Carmo       | <https://github.com/GCarmo4>     | <mailto:goncalo.n.carmo@tecnico.ulisboa.pt>             |
| 100120  | Alexandre Coelho     | <https://github.com/alexfaisca> | <mailto:alexandre.f.coelho@tecnico.ulisboa.pt>         |

## Getting Started

The overall system is made up of several modules. The main server is the _DistLedgerServer_. The clients are the _User_ 
and the _Admin_. The definition of messages and services is in the _Contract_. The future naming server
is the _NamingServer_.

See the [Project Statement](https://github.com/tecnico-distsys/DistLedger) for a complete domain and system description.

### Prerequisites

The Project is configured with Java 17 (which is only compatible with Maven >= 3.8), but if you want to use Java 11 you
can too -- just downgrade the version in the POMs.

To confirm that you have them installed and which versions they are, run in the terminal:

```s
javac -version
mvn -version
```

### Installation

To compile and install all modules:

```s
mvn clean install
```

## Built With

* [Maven](https://maven.apache.org/) - Build and dependency management tool;
* [gRPC](https://grpc.io/) - RPC framework.
