# Reflection
## Commit 1
Pertama, pada method handle_connection kita menerima parameter stream yang berguna untuk membaca data dari TCP Stream. Pada baris pertama dari method handle_connection yang merupakan potongan kode dibawah ini, kita membuat sebuah BufReader baru untuk menghandle pembacaan IO dari stream. 

```
let buf_reader = BufReader::new(&mut stream);
```

Kemudian, baris kedua dari method handle_connection yang merupakan potongan kode dibawah ini, kita membuat variabel http_request untuk mengumpulkan request yang kita kirim ke server (yang di mana pada kasus ini ke http:127.0.0.1:7878). 

```
let http_request: Vec<_> = buf_reader
    .lines()
    .map(|result| result.unwrap())
    .take_while(|line| !line.is_empty())
    .collect();
```

Karena terdapat deklarasi Vec<_> maka kita akan menyimpan request yang dikirim ke Vector tersebut. Fungsi .lines() berguna untuk memisahkan String data dari stream ketika bertemu dengan \n. Kemudian, untuk mendapatkan setiap String yang ada, kita melakukan map dan unwrap setiap dari String tersebut yang di mana kita memanfaatkan result untuk unwrap tersebut. Setelah itu, .take_while(|line| !line.is_empty()) akan berhenti ketika dia menemukan line yang kosong dan setelah berhenti maka kita akan menggabungkan semua hasil ke Vector tersebut.

Dan terakhir, kita akan print output dari http_request tersebut.
```
println!("Request: {:#?}", http_request);
```