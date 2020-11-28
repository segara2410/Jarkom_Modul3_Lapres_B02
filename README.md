1\. Membuat topologi jaringan. Disini terdapat 3 switch, 4 client, 1
router, dan 3 server

![](.//media/image1.png)

Setting Surabaya sebagai router dengan interface eth0, eth1, eth2, eth3.

![](.//media/image2.png)

Lalu setting Gresik sebagai client.

![](.//media/image3.png)

Setting Sidoarjo sebagai client.

![](.//media/image4.png)

Setting Banyuwangi sebagai client.

![](.//media/image5.png)

Setting Madiun sebagai client.

![](.//media/image6.png)

Setting Malang sebagai server.

![](.//media/image7.png)

Setting Mojokerto sebagai server.

![](.//media/image8.png)

Setting Tuban sebagai server.

![](.//media/image9.png)

2\. Buat Surabaya sebagai DHCP Relay. Install isc dhcp relay pada
Surabaya, lalu untuk settingannya server diarahkan ke Tuban dan
interfacenya adalah eth1, eth2, eth3.

![](.//media/image10.png)

Lalu pada Tuban interfacenya di buat eth0

![](.//media/image11.png)

Lalu untuk subnetnya diarahkan ke ip router. 

3\. Untuk client Gresik
dan Sidoarjo di setting subnet mendapat ip dengan range dari
192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai
192.168.0.200. 

4\. Dan untuk Banyuwangi dan Madiun dengan range
192.168.1.50 sampai 192.168.1.70.

![](.//media/image12.png)

Lalu di test apakah masing-masing Client telah mendapatkan IP setelah
semua Client di setting IP dinamis dari DHCP.

![](.//media/image13.png)

![](.//media/image14.png)

![](.//media/image15.png)

![](.//media/image16.png)

5\. Cek apakah masing=masing Client telah mendapatkan DNS dengan melihat resolv.conf semua client.

![](.//media/image17.png)

![](.//media/image18.png)

![](.//media/image19.png)

![](.//media/image20.png)

6\. Pada dhcpd.conf untuk subnet 1 diberi default dan max lease time 300
detik. Dan subnet 3 600 detik.

![](.//media/image12.png)

7\. Pertama nyalakan proxy dengan IP Mojokerto. Lalu untuk membuat user
authentikasi dengan passwd.

![](.//media/image21.png)

Hasilnya setelah membuat user authentikasi

![](.//media/image22.png)

**8.** Agar internet hanya bisa di akses pada Selasa-Rabu pukul 13:00 --
18:00 maka perlu membuat acl KERJA_TA dengan settingan seperti dibawah.
**9.** Lalu untuk akses Selasa-Kamis 21:00 -- 09:00 (sampai jumat jam
09:00) membuat acl BIMBINGAN_MALAM dan BIMBINGAN_PAGI.

![](.//media/image23.png)

Lalu di squid.conf, untuk nomer **7.** Perlu ditambahkan auth_param yang
diarahkan pada passwd yang telah dibuat. Untuk nomer **8** dan **9.**
Ditambahkan http_access allow untuk KERJA_TA, BIMBINGAN_MALAM,
BIMBINGAN_PAGI yang di AND kan dengan USERS.

**10.** ditambahkan acl BAN dengan access deny untuk google.com dan
diarahkan ke monta.if.its.ac.id

![](.//media/image24.png)

Saat mengakses google.com

![](.//media/image25.png)

11\. download dengan wget dan letakkan di ERR_ACCESS_DENIED

![](.//media/image26.png)

Hasilnya saat mengakses web yg tidak bisa diakses.

![](.//media/image27.png)

12\. Membuat DNS di malang yang diarahakan ke IP Mojokerto.

![](.//media/image28.png)

![](.//media/image29.png)

Lalu pada saat menyalakan proxy bisa mengganti IP Mojokerto dengan
menggunakan janganlupa-ta.b02.pw. Hasilnya,

![](.//media/image22.png)
