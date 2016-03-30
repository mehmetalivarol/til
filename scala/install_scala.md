## How to install Scala on CentOS

    wget http://www.scala-lang.org/files/archive/scala-2.10.1.tgz
    tar xvf scala-2.10.1.tgz
    sudo mv scala-2.10.1 /usr/lib
    sudo ln -s /usr/lib/scala-2.10.1 /usr/lib/scala
    export PATH=$PATH:/usr/lib/scala/bin
    scala -version

