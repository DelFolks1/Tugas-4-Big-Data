
<h1> Kafka Infrastruktur </h1>
Nama : Raja Permata Boy <br>
NRP : 05111740000070 <br>

1. Lakukan instalasi Docker pada desktop. <br>
<img src="/doc/installdocker.jpg"><br>
2. Pembuatan Infrastruktur.Kita dapat menggunakan: <br>
- Docker command<br>
  Kita mengeksekusi satu per satu pembuatan containernya.<br>
- Docker compose<br>
  Kita menggunakan Dockerfile untuk menentukan container apa saja yang akan dibuat. Docker secara otomatis membuatkan semua container         sesuai dengan dependency yang kita tentukan.<br>
3. Saya akan menggunakan docker-compose dalam membangun infrastruktur Kafka<br>
4. Buat script docker-compose.yml yang berisi : <br>
    version: '2'<br>

    networks:<br>
      kafka-net:<br>
        driver: bridge<br>
    
    services:<br>
      zookeeper-server:<br>
        image: 'bitnami/zookeeper:latest'<br>
        networks:<br>
          - kafka-net<br>
        ports:<br>
          - '2181:2181'<br>
        environment:<br>
          - ALLOW_ANONYMOUS_LOGIN=yes<br>
      kafka-server1:<br>
        image: 'bitnami/kafka:latest'<br>
        networks:<br>
          - kafka-net<br>    
        ports:<br>
          - '9092:9092'<br>
        environment:<br>
          - KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper-server:2181<br>
          - KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092<br>
          - ALLOW_PLAINTEXT_LISTENER=yes<br>
        depends_on:<br>
          - zookeeper-server<br>
      kafka-server2:<br>
        image: 'bitnami/kafka:latest'<br>
        networks:<br>
          - kafka-net<br>    
        ports:<br>
          - '9093:9092'<br>
        environment:<br>
          - KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper-server:2181<br>
          - KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9093<br>
          - ALLOW_PLAINTEXT_LISTENER=yes<br>
        depends_on:<br>
          - zookeeper-server<br>
5. Buka docker, maka akan belum ada kontainer yang terlihat<br>
6. Lalu masuk ke direktori dimana file docker-compose.yml tadi berada. Lalu jalankan script dengan command docker-compose up -d<br>
<img src="/doc/cmd.jpg"><br>
7. Infrastruktur kafka berhasil dibuat<br>
<img src="/doc/container.jpg"><br>
8. Untuk testing, kita dapat menggunakan aplikasi Conduktor. Testing bertujuan untuk mengecek apakah kafka yg sudah kita buat dapat kita gunakan<br>
<img src="/doc/conduktor.jpg"><br>
9. Buat konfigurasi cluster, kemudian tekan save, setelah itu hubungkan dengan cluster yang telah dibuat.<br>
 <img src="/doc/conduktor2.jpg"><br>
